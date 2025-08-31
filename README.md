# t1# Playbook: Sistema Cliente-Servidor na Nuvem Pública

Este documento descreve todos os passos para criar o ambiente completo do projeto web com Apache, PHP e MariaDB no **Ubuntu Server**.

---

## 1️⃣ Atualizar o sistema

```bash
sudo apt update
sudo apt upgrade -y

sudo apt install apache2 php libapache2-mod-php php-mysql -y

sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl status apache2

sudo apt install mariadb-server mariadb-client -y
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo systemctl status mariadb

sudo mysql_secure_installation

sudo mysql -u root -p

CREATE DATABASE portfolio;
CREATE USER 'portuser'@'localhost' IDENTIFIED BY '123atv';  -- substitua pela sua senha real
GRANT ALL PRIVILEGES ON portfolio.* TO 'portuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;

USE portfolio;

CREATE TABLE mensagens (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100),
    mensagem TEXT
);

sudo cp index.html processa.php listar.php /var/www/html/

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

curl http://localhost/index.html
curl -d "nome=Teste&email=teste@email.com&mensagem=Teste" -X POST http://localhost/processa.php
curl http://localhost/listar.php