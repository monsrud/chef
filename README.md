<pre>

These are some chef resource examples that may be commonly used to configure hosts.

# execute a command
execute 'apache_configtest' do
 command '/usr/sbin/apachectl configtest'
end

# install a package
package 'name' do
  action :install
end

# install multiple packages
%w{gcc make nginx mysql}.each do |pkg|
   package pkg do
      action :install
   end
end

# install a specific package per os type
package 'Install Apache' do
  case node[:platform]
  when 'redhat', 'centos'
    package_name 'httpd'
  when 'ubuntu', 'debian'
    package_name 'apache2'
  end
end



# add a user
user 'frank' do
  home '/home/frank'
  shell '/bin/bash'
  password '$1$JJsvHslasdfjVEroftprNn4JHtDi'
end

# set the timezone
timezone 'name' do
  timezone      String # default value: 'name' unless specified
  action        Symbol # defaults to :set if not specified
end


# copy a file from the cookbook to a node
# https://docs.chef.io/resources/cookbook_file/
# A cookbook_file resource block manages files by using files that exist within a cookbook’s /files directory. For example, to write the home page for an Apache # website:



cookbook_file '/var/www/customers/public_html/index.php' do
  source 'index.php'
  owner 'web_admin'
  group 'web_admin'
  mode '0755'
  action :create
end

# the content of a file can also be provided inline
file '/var/www/customers/public_html/index.php' do
  content '<html>This is a placeholder for the home page.</html>'
  mode '0755'
  owner 'web_admin'
  group 'web_admin'
end

# service resource start/stop/enable/disable
service 'rpcbind' do
  action [:start, :enable]
  supports status: true
end

# configure the host name
hostname 'name' do
  fqdn                 String
  hostname             String # default value: 'name' unless specified
  ipaddress            String # default value: The node's IP address as determined by Ohai.
  action               Symbol # defaults to :set if not specified
end

# reboot a host
reboot 'name' do
  delay_mins      Integer # default value: 0
  reason          String # default value: "Reboot by Chef Infra Client"
  action          Symbol # defaults to :nothing if not specified
end


# group resource : work with unix groups
# git resource : work with git repos
# link resource : create hard or soft links
# sudo resource : modify sudo users
