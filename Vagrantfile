# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    ### change these two parameters unique to your project!
    #================================================================

    hostname = "scotchbox"
    ip = "192.168.33.10"

    #================================================================


    config.vm.network "private_network", ip: "#{ip}"
    config.vm.hostname = hostname
    config.vm.box = "scotch/box"
    config.hostsupdater.aliases = ["www.#{hostname}.dev","#{hostname}.dev"]
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
    
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    # to get WordPress up and running
    config.vm.provision "shell", inline: <<-SHELL
        composer self-update
        cd /tmp && sudo wget -q https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && sudo chmod +x /tmp/wp-cli.phar && sudo mv /tmp/wp-cli.phar /usr/local/bin/wp
        cd /var/www/ && git clone https://github.com/roots/bedrock.git #{hostname}.dev
        rm -Rf /var/www/#{hostname}.dev/.git
        cd /var/www/#{hostname}.dev && composer update
        sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/#{hostname}.dev.conf
        sudo sed -i "s/public/#{hostname}.dev\\/web/g" /etc/apache2/sites-available/#{hostname}.dev.conf
        sudo sed -i "s/#ServerName www.example.com/ServerName #{hostname}.dev/g" /etc/apache2/sites-available/#{hostname}.dev.conf
        sudo a2ensite #{hostname}.dev
        sudo service apache2 reload
        printf "DB_NAME=scotchbox\nDB_USER=root\nDB_PASSWORD=root\nDB_HOST=127.0.0.1\nWP_ENV=development\nWP_HOME=http://#{hostname}.dev\nWP_SITEURL=http://#{hostname}.dev/wp" > /var/www/#{hostname}.dev/.env
        cd /var/www/#{hostname}.dev/web && wp core install --allow-root --url=http://#{hostname}.dev --title=#{hostname} --admin_user=admin --admin_password=admin --admin_email=admin@#{hostname}.dev --quiet
        cd /var/www/ && git add #{hostname}.dev
    SHELL

    config.vm.provider :virtualbox do |vb|
		    vb.gui = false
		    vb.memory = 1024
        vb.name = hostname
        vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
        vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
    end

end
