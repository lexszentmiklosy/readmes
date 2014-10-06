Setting up Sparse Checkout in Git to only pull static html site

cd /var/www #Change to Apache Directory
sudo rm -Rf html #Remove the old html directory
sudo git init #Make the current directory a git repo
sudo git remote add origin https://bitbucket.org/dmgdirectv/$project_name.git #Tie the git repo to the project
sudo git config core.sparsecheckout true #setup sparse checkout
sudo nano .git/info/sparse-checkout #open the text editor to add the html directory to the sparce checkout file

	html/
	
ctrl+x,  y, enter #exit, save, commit
sudo git pull origin master #pull just the html directory and you are done!




Setting up ModRewrite to remove extensions.
website.com/index.html = website.com/index = website.com/index/

sudo a2enmod rewrite #Install mod-rewrite 
sudo service apache2 restart #Restart Apache
sudo nano /etc/apache2/apache2.conf #Open apache Conf in text editor. 
	
	Directory/var/ww
	AllowOverride FileInfo
	
ctrl+x,  y, enter #exit, save, commit
cd /var/www/html #Change to Apache Directory
sudo nano .htaccess # open config file for rewrites

	RewriteEngine On

	RedirectMatch 301 ^(.+)/$ $1

	#example.com/page will display the contents of example.com/page.html
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_FILENAME}.html -f
	RewriteRule ^(.+)$ $1.html [L,QSA]

	#301 from example.com/page.html to example.com/page
	RewriteCond %{THE_REQUEST} ^[A-Z]{3,9}\ /.*\.html\ HTTP/
	RewriteRule ^(.*)\.html$ /$1 [R=301,L]

ctrl+x,  y, enter

