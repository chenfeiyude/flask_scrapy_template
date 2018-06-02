============================================================================================================
To extend a new spider. See the existing spider examples in ./spiders/

1. Create your own spider in ./spiders/spider_robot/spiders like the existing spiders
2. Create your own items in ./spiders/spider_robot/items.py, the item depends on what your original data have.
3. Configure your spider in ./spiders/spider_manager.py  and ./common/constants.py
4. Add your new spider in table spider_configure or put in flask_scrapy_manager.py deploy method
    e.g INSERT IGNORE INTO `spider_configure` (`spider_name`) VALUES ('nct');
============================================================================================================
To deploy this python project

1. install sqlite
sudo yum install sqlite-devel -y

2. if missing Twisted
wget https://pypi.python.org/packages/source/T/Twisted/Twisted-15.2.1.tar.bz2
tar -xjvf Twisted-15.2.1.tar.bz2
cd Twisted-15.2.1
python setup.py install

3.sudo yum install -y libffi libffi-devel libxslt-devel libxml2-devel

4. install python2.7 
wget http://www.python.org/ftp/python/2.7.6/Python-2.7.6.tgz
tar -xzf Python-2.7.6.tgz  
cd Python-2.7.6
./configure --prefix=/usr/local
make && make install
python2.7 setup install

5. install tools easy_install-2.7
wget http://pypi.python.org/packages/source/d/distribute/distribute-0.6.35.tar.gz
tar xf distribute-0.6.35.tar.gz
cd distribute-0.6.35
python2.7 setup.py install

6. install pip2.7
easy_install-2.7 pip

7. go to project package/
virtualenv --no-site-packages venv
source venv/bin/activate
pip2.7 install -r requirements.txt

(ignore)8.install firefox, the scrapy lib needs a browser driver
sudo yum install firefox

(ignore)9.Xvfb is a software that simulates a display doing everything in memory and not showing any screen output.
sudo yum install xorg-x11-server-Xvfb

10. deploy & run the server
# only first time deploy need to deploy migrate database
python2.7 flask_scrapy_manage.py db init
python2.7 flask_scrapy_manage.py db migrate
python2.7 flask_scrapy_manage.py db upgrade
python2.7 flask_scrapy_manage.py deploy

./start_flask_scrapy.sh


11. install httpie for testing
pip install httpie

e.g testing like
# http --auth username:secret_key GET http://localhost:5002/api/v1.0/test_flask_scrapy key=some_search_key get_latest=True





