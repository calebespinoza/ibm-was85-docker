FROM centos:7

ARG ibmUser=myIBMuser
ARG ibmPass=myIBMpass
ARG passphrase=myPassphrase
RUN yum install glibc.i686 elfutils-libelf.i686 elfutils-lib.i686 elfutils-libelf-devel.i686 \
    elfutils-libelf-devel-static.i686 libgcc-4.8.5-39.el7.i686 unzip wget -y --disableexcludes=all
#RUN yum install libgcc-4.8.5-39.el7.i686 unzip wget -y
RUN wget --user ${ibmUser} --password ${ibmPass}} -O /opt/ibmim.zip https://ak-delivery04-mul.dhe.ibm.com/sdfdl/v2/sar/CM/RA/08mvd/0/Xa.2/Xb.jusyLTSp44S03pYBmsDvhD9IqGeCC7OEOngL5hH9mgG942BqlbTiPUBGqcw/Xc.CM/RA/08mvd/0/agent.installer.linux.gtk.x86_1.9.1001.20191112_1525.zip/Xd./Xf.LPR.D1VC/Xg.10613103/Xi.habanero/XY.habanero/XZ.aJXkWek4CN8IXfpu-mB9DK2KKKw/agent.installer.linux.gtk.x86_1.9.1001.20191112_1525.zip
RUN mkdir /opt/ibmim
RUN unzip /opt/ibmim.zip -d /opt/ibmim
RUN /opt/ibmim/installc -acceptLicense
RUN rm -rf /opt/ibmim
RUN rm -f /opt/ibmim.zip
RUN touch /opt/credential.store
RUN touch /opt/master_password_file.txt
RUN echo ${passphrase} > /opt/master_password_file.txt
WORKDIR /opt/IBM/InstallationManager/eclipse/tools
RUN ./imutilsc saveCredential -url http://www.ibm.com/software/repositorymanager/com.ibm.websphere.DEVELOPERSILAN.v85 -userName ${ibmUser} -userPassword ${ibmPass} -secureStorageFile /opt/credential.store -masterPasswordFile /opt/master_password_file.txt
RUN ./imcl install com.ibm.websphere.DEVELOPERSILAN.v85 -repositories http://www.ibm.com/software/repositorymanager/com.ibm.websphere.DEVELOPERSILAN.v85 -acceptLicense -properties user.wasjava=java8 -showProgress -record install_was.xml -installFixes recommended -secureStorageFile /opt/credential.store -masterPasswordFile /opt/master_password_file.txt

# STORING CREDENTIALS
# https://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.4/com.ibm.cic.commandline.doc/topics/t_imcl_store_credentials.html

# imcl COMMANDO ARGUMENTS
# https://www.ibm.com/support/knowledgecenter/en/SSDV2W_1.8.4/com.ibm.cic.commandline.doc/topics/r_tools_imcl.html