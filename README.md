
# execute a command
execute 'apache_configtest' do
  command '/usr/sbin/apachectl configtest'
end

# install a package

package 'name' do
  action :install
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
