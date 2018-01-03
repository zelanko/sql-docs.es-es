---
title: "Configuración de PolyBase | Microsoft Docs"
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: "17"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 07ace3fa24747619e8dbe64cbeb461175220a755
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="polybase-configuration"></a>Configuración de PolyBase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice los procedimientos siguientes para configurar PolyBase.  
  
## <a name="external-data-source-configuration"></a>Configuración del origen de datos externo  
 Debe asegurarse de que funciona correctamente la conectividad desde SQL Server al origen de datos externo. El tipo de conectividad influye significativamente en el rendimiento de las consultas. Por ejemplo, un vínculo de 10 Gigabit Ethernet producirá un tiempo de respuesta de consulta menor en las consultas PolyBase que uno de 1 Gigabit Ethernet.  
  
 Debe configurar SQL Server para conectarse a la versión de Hadoop o a Almacenamiento de blobs de Azure con **sp_configure**. PolyBase es compatible con dos distribuciones de Hadoop: Hortonworks Data Platform (HDP) y Cloudera Distributed Hadoop (CDH).  Para obtener una lista completa de los orígenes de datos externos compatibles, vea [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
1 Nota: PolyBase no admite las zonas cifradas de Cloudera. 
  
### <a name="run-spconfigure"></a>Ejecución de sp_configure  
  
1.  Ejecute la “conectividad de hadoop” sp_configure y defina un valor adecuado.  Para hallar el valor, vea [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
    ```sql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  Debe reiniciar SQL Server con **services.msc**. Al reiniciar SQL Server, se reinician estos servicios:  
  
    -   Servicio de movimiento de datos de SQL Server PolyBase  
  
    -   Motor de SQL Server PolyBase  
  
## <a name="pushdown-configuration"></a>Aplicación de la configuración  
 Para mejorar el rendimiento de las consultas, habilite el cálculo de la aplicación a un clúster de Hadoop que necesita para proporcionar a SQL Server algunos parámetros de configuración específicos del entorno de Hadoop:  
  
1.  Busque el archivo **yarn-site.xml** en la ruta de acceso de instalación de SQL Server. Normalmente, la ruta de acceso es:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  En el equipo de Hadoop, busque el archivo análogo en el directorio de configuración de Hadoop. En el archivo, busque y copie el valor de la clave de configuración yarn.application.classpath.  
  
3.  En el equipo de SQL Server, en el **archivo yarn.site.xml,** busque la propiedad **yarn.application.classpath** . Pegue el valor de la máquina de Hadoop en el elemento de valor.  

4. Para todas las versiones 5.X de CDH, deberá agregar los parámetros de **mapreduce.application.classpath** al final del archivo **yarn.site.xml** o en el archivo **mapred-site.xml file**. HortonWorks incluye estas configuraciones dentro de las configuraciones **yarn.application.classpath**.

## <a name="connecting-to-hadoop-cluster-with-hadooprpcprotection-setting"></a>Conectarse al clúster de Hadoop con la opción de configuración Hadoop.RPC.Protection
Una forma habitual de proteger la comunicación en un clúster de Hadoop consiste en cambiar la configuración de hadoop.rpc.protection a "Privacy" (Privacidad) o "Integrity" (Integridad). De forma predeterminada, PolyBase da por hecho que la configuración está establecida en "Authenticate" (Autenticar). Para reemplazar esta configuración predeterminada, debe agregar la siguiente propiedad al archivo core-site.xml. Cambiar esta configuración permitirá efectuar una transferencia de datos segura entre los nodos de Hadoop y permitirá establecer una conexión SSL con SQL Server.

```
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
  <property>
    <name>hadoop.rpc.protection</name>
    <value></value>
  </property> 
```




## <a name="example-yarn-sitexml-and-mapred-sitexml-files-for-cdh-5x-cluster"></a>Archivos de ejemplo yarn-site.xml y mapred-site.xml para el clúster CDH 5.X.



Yarn-site.xml con la configuración yarn.application.classpath y mapreduce.application.classpath.
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>

```
Si decide dividir las dos opciones de configuración en mapred-site.xml y yarn-site.xml, los archivos serían los siguientes:

**yarn-site.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

**mapred-site.xml**

Tenga en cuenta que hemos agregado la propiedad mapreduce.application.classpath. En CDH 5.x, encontrará los valores de configuración en la misma convención de nomenclatura de Ambari.

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
  <property>
    <name>mapred.min.split.size</name>
      <value>1073741824</value>
  </property>
  <property>
    <name>mapreduce.app-submission.cross-platform</name>
    <value>true</value>
  </property>
<property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
  </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
    <name>mapreduce.jobhistory.principal</name>
    <value></value>
  </property>
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value></value>
  </property>
-->
</configuration>
  
```
  
## <a name="kerberos-configuration"></a>Configuración de Kerberos  
Tenga en cuenta que cuando PolyBase se autentica en un clúster protegido de Kerberos, se requiere establecer la configuración de hadoop.rpc.protection para la autenticación. Esta acción dejará la comunicación de datos entre los nodos Hadoop sin cifrar. 

 Para conectarse a un clúster de Hadoop protegido con Kerberos [con MIT KDC]:
   
  
1.  Busque el directorio de configuración de Hadoop en la ruta de acceso de instalación de SQL Server. Normalmente, la ruta de acceso es:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Busque el valor de configuración del lado de Hadoop de las claves de configuración que se muestran en la tabla. (En el equipo de Hadoop, busque los archivos en el directorio de configuración de Hadoop).  
  
3.  Copie los valores de configuración en la propiedad Value en los archivos correspondientes en el equipo de SQL Server.  
  
    |**#**|**Archivo de configuración**|**Clave de configuración**|**Acción**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique el nombre de host KDC. Por ejemplo: kerberos.su-dominio.com.|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique el dominio Kerberos. Por ejemplo: SU-DOMINIO.COM|  
    |3|core-site.xml|hadoop.security.authentication|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: KERBEROS<br></br>**Nota de seguridad:** KERBEROS debe estar en mayúsculas. Si aparece en minúsculas, puede que no esté activado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, yarn/_HOST@YOUR-REALM.COM|  
  
4.  Cree un objeto de credencial con ámbito de base de datos para especificar la información de autenticación para cada usuario de Hadoop. Vea [PolyBase T-SQL objects (Objetos T-SQL de PolyBase)](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Objetos T-SQL de PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Ver también  
 [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  
