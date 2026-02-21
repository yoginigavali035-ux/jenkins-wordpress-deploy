pipeline {
    agent any

    environment {
        SSH_CRED    = 'wordpress-app-key'
        SERVER_IP   = '172.31.40.143'
        REMOTE_USER = 'ubuntu'
        WEB_DIR     = '/var/www/html'

        DB_NAME     = 'wordpress'
        DB_USER     = 'wpuser'
        DB_PASS     = 'wppassword123'
    }

    stages {

        stage('Deploy WordPress with DB Config') {
            steps {
                sshagent(credentials: ["${SSH_CRED}"]) {
                    sh '''
                        echo "Installing Apache, MySQL, PHP..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            sudo apt update -y &&
                            sudo apt install apache2 mysql-server php php-mysql libapache2-mod-php wget unzip -y
                        "

                        echo "Creating MySQL Database..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            sudo mysql -e \\"CREATE DATABASE IF NOT EXISTS ${DB_NAME};\\"
                            sudo mysql -e \\"CREATE USER IF NOT EXISTS '${DB_USER}'@'localhost' IDENTIFIED BY '${DB_PASS}';\\"
                            sudo mysql -e \\"GRANT ALL PRIVILEGES ON ${DB_NAME}.* TO '${DB_USER}'@'localhost';\\"
                            sudo mysql -e \\"FLUSH PRIVILEGES;\\"
                        "

                        echo "Cleaning old website files..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            sudo rm -rf ${WEB_DIR}/*
                        "

                        echo "Downloading WordPress..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            cd /tmp &&
                            wget -q https://wordpress.org/latest.zip &&
                            unzip -o latest.zip
                        "

                        echo "Moving WordPress files..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            sudo cp -r /tmp/wordpress/* ${WEB_DIR}/
                        "

                        echo "Configuring wp-config.php..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            cd ${WEB_DIR}
                            sudo cp wp-config-sample.php wp-config.php
                            sudo sed -i \\"s/database_name_here/${DB_NAME}/\\" wp-config.php
                            sudo sed -i \\"s/username_here/${DB_USER}/\\" wp-config.php
                            sudo sed -i \\"s/password_here/${DB_PASS}/\\" wp-config.php
                        "

                        echo "Setting permissions..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            sudo chown -R www-data:www-data ${WEB_DIR}
                            sudo chmod -R 755 ${WEB_DIR}
                            sudo systemctl restart apache2
                        "
                    '''
                }
            }
        }
    }
}