yum install wget rsync maven java java-devel rpm-build gcc -y
yum install ntp python python-devel rpm-build gcc-c++ git -y
# yum install java-1.7.0-openjdk java-1.7.0-openjdk-devel -y

wget https://pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg#md5=fe1f997bc722265116870bc7919059ea
# (exsist)
sh setuptools-0.6c11-py2.7.egg

wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -P /tmp
# (exsist)
tar xf /tmp/apache-maven-3.6.3-bin.tar.gz -C /opt
ln -s /opt/apache-maven-3.6.3 /opt/maven
nano /etc/profile.d/maven.sh
chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh
mvn -v # Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)

wget https://downloads.apache.org/ambari/ambari-2.7.5/apache-ambari-2.7.5-src.tar.gz
# (exsist)
tar xfvz apache-ambari-2.7.5-src.tar.gz
cd apache-ambari-2.7.5-src
cd ambari-admin
yum --enablerepo=extras install epel-release
# (exsist)
yum install npm -y
node -v # v10.24.1
npm -v # 6.14.12
vi pom.xml # edit node and npm version
cd ..
mvn versions:set -DnewVersion=2.7.5.0.0
pushd ambari-metrics
mvn versions:set -DnewVersion=2.7.5.0.0
popd
# mvn -B clean install rpm:rpm -DnewVersion=2.7.5.0.0 -DbuildNumber=5895e4ed6b30a2da8a90fee2403b6cab91d19972 -DskipTests -Dpython.ver="python >= 2.7"
mvn -B clean install rpm:rpm -Drat.skip=true -DnewVersion=2.7.5.0.0 -DbuildNumber=5895e4ed6b30a2da8a90fee2403b6cab91d19972 -DskipTests -Dpython.ver="python >= 2.7" -e
yum install /root/apache-ambari-2.7.5-src/ambari-server/target/rpm/ambari-server/RPMS/x86_64/ambari-server-2.7.5.0-0.x86_64.rpm
yum install /root/apache-ambari-2.7.5-src/ambari-agent/target/rpm/ambari-agent/RPMS/x86_64/ambari-agent-2.7.5.0-0.x86_64.rpm