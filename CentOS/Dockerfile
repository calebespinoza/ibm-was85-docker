FROM centos:7
LABEL mantainer="Caleb Espinoza Gutierrez"
LABEL twitter="@caleblogs"

# Set ARGuments
ARG ibmUser=myIBMuser
ARG ibmPass=myIBMpass
ARG passphrase=myPassphrase
ARG wasProfileUser=admin
ARG wasProfilePass=admin
ARG ibmIMUrl=https://ak-delivery04-mul.dhe.ibm.com/sdfdl/v2/sar/CM/RA/08mvd/0/Xa.2/Xb.jusyLTSp44S03pYBmsDvhD9IqGeCC7OEOngL5hH9mgG942BqlbTiPUBGqcw/Xc.CM/RA/08mvd/0/agent.installer.linux.gtk.x86_1.9.1001.20191112_1525.zip/Xd./Xf.LPR.D1VC/Xg.10613103/Xi.habanero/XY.habanero/XZ.aJXkWek4CN8IXfpu-mB9DK2KKKw/agent.installer.linux.gtk.x86_1.9.1001.20191112_1525.zip
ARG wasRepo=http://www.ibm.com/software/repositorymanager/com.ibm.websphere.DEVELOPERSILAN.v85

# Install dependencies
RUN yum install glibc.i686 elfutils-libelf.i686 elfutils-lib.i686 elfutils-libelf-devel.i686 \
    elfutils-libelf-devel-static.i686 libgcc-4.8.5-39.el7.i686 unzip wget -y --disableexcludes=all

# Download IBM Installatiion Manager installer
RUN wget --user ${ibmUser} --password ${ibmPass} -O /opt/ibmim.zip ${ibmIMUrl}

# Install IBM Installation Manager
RUN mkdir /opt/ibmim && unzip /opt/ibmim.zip -d /opt/ibmim
RUN /opt/ibmim/installc -acceptLicense
RUN rm -rf /opt/ibmim && rm -f /opt/ibmim.zip

# Store IBM Credentials
RUN touch /opt/credential.store && touch /opt/master_password_file.txt
RUN echo ${passphrase} > /opt/master_password_file.txt
WORKDIR /opt/IBM/InstallationManager/eclipse/tools
RUN ./imutilsc saveCredential -url ${wasRepo} -userName ${ibmUser} -userPassword ${ibmPass} \
    -secureStorageFile /opt/credential.store -masterPasswordFile /opt/master_password_file.txt

# Install IBM Websphere Application Server
RUN ./imcl install com.ibm.websphere.DEVELOPERSILAN.v85 \
    -repositories ${wasRepo} -acceptLicense -properties user.wasjava=java8 \
    -showProgress -record install_was.xml -installFixes recommended \
    -secureStorageFile /opt/credential.store -masterPasswordFile /opt/master_password_file.txt

# Delete Credentials Stored
RUN rm -f /opt/credential.store && rm -f /opt/master_password_file.txt

# Create a WAS profile AppSrv01
WORKDIR /opt/IBM/WebSphere/AppServer/bin
RUN ./manageprofiles.sh -create -profileName AppSrv01 \
    -profilePath "/opt/IBM/WebSphere/AppServer/profiles/AppSrv01" \
    -templatePath "/opt/IBM/WebSphere/AppServer/profileTemplates/default" \
    -enableAdminSecurity true -adminUserName ${wasProfileUser} -adminPassword ${wasProfilePass}

RUN cat /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/logs/AboutThisProfile.txt

ENTRYPOINT [ "/opt/IBM/WebSphere/AppServer/bin/startServer.sh" ]
CMD [ "server1" ]
