require 'aws-sdk'
require 'fileutils'

ROOT_DIR = File.dirname(__FILE__)
TARGET_DIR = File.join( ROOT_DIR, "_site" )

CONTENT_TYPES = {
  ".xml"  => "text/xml",
  ".txt"  => "text/plain",
  ".js"   => "text/javascript",
  ".css"  => "text/css",
  ".html" => "text/html",
  ".jpg"  => "image/jpeg"
}


def bucket
  AWS::S3.new.buckets[@config['s3_bucket']]
end


def remote_obj( path )
  bucket.objects[path]
end


desc "Builds and uploads the website."
task :default => [:build, :upload]


task :init do  
  config_path = File.join( ROOT_DIR, '.upload.cfg.yml' )
  unless File.exists? config_path
    puts "Could not find #{config_path}."
    exit
  end

  env = ENV['SITE'] || 'test'
  @config = YAML.load_file( config_path )[env]

  AWS.config(:access_key_id => @config['aws_access_key_id'], :secret_access_key => @config['aws_secret_access_key'])
end


desc "Deletes the locally generated files in #{TARGET_DIR}"
task :clean do
  FileUtils.rm_r( TARGET_DIR ) if Dir.exists?( TARGET_DIR )
end


desc "Builds a fresh site into #{TARGET_DIR}"
task :build => [:clean] do
  puts `jekyll`
end


desc "Uploads all files from #{TARGET_DIR}"
task :upload => [:init] do

  if ENV['FROM']
    # single file
    upload_file( ENV['FROM'], remote_obj(ENV['TO']) )
  else
    # everything!
    path_pairs = []

    Dir["#{TARGET_DIR}/**/**"].each do |local_path|
      # skip directories
      next if File.directory?( local_path )
      
      # convert to remote paths
      remote_path = local_path.gsub( "#{TARGET_DIR}/", '' )

      path_pairs << [local_path, remote_obj(remote_path)]
    end

    upload_set( path_pairs )
  end
end


def upload_set( path_pairs, uploaders = 2 )
  require 'ruby-progressbar'

  progress_bar = ProgressBar.create( :title => "Uploading", :total => path_pairs.length, :format => "%t %c/%C %b" )
 
  # divide up the path pairs
  chunks = path_pairs.each_slice( uploaders ).to_a

  threads = chunks.collect do |c|
    Thread.new do
      while c.length > 0
        local, remote = c.pop
        upload_file( local, remote, true ) # silent mode
        progress_bar.increment
      end
    end
  end

  threads.collect { |t| t.join }
end


def upload_file( local_path, remote_object, silent = false )
  data = File.open(local_path).read
  content_type = CONTENT_TYPES[ File.extname( local_path ) ]
  
  puts "uploading #{remote_object.key} as #{content_type}" unless silent
  remote_object.write( data, :content_type => content_type )
end


desc "Deletes a remote site, with confirmation."
task :napalm => [:init] do
  print "Are you absolutely sure you wish to nuke the contents of #{@config['s3_bucket']}? [y/N] "
  if STDIN.gets =~ /y/i
    puts "\nDeleting. Hang tight ..."
    bucket.objects.each do |o|
      puts "deleting #{@config['s3_bucket']}/#{o.key}"
      o.delete
    end
  end
end
