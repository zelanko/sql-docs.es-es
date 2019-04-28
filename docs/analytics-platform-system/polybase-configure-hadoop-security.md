---
title: Configurar la seguridad de PolyBase Hadoop en Analytics Platform System | Microsoft Docs
description: Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop externo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c916fef2b70333c2d5bc89fec5c86d61482cdba7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678613"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Configuración y seguridad de PolyBase para Hadoop

En este artículo se proporciona una referencia para distintos valores de configuración que afectan a la conectividad de PolyBase de puntos de acceso a Hadoop. Para ver un tutorial sobre las novedades de PolyBase, consulte [¿qué es PolyBase](configure-polybase-connectivity-to-external-data.md).

> [!NOTE]
> En los puntos de acceso, los cambios en archivos XML son necesarios en todos los nodos de proceso y el nodo de control.
> 
> Tenga especial cuidado al modificar los archivos XML de APS. Las etiquetas que faltan o caracteres no deseados pueden invalidar el archivo xml que se reducen lo usablilty de la característica.
> Los archivos de configuración de Hadoop se encuentran en la ruta de acceso siguiente:  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> Los cambios en los archivos xml requieren un reinicio del servicio para ser efectivo.

## <a id="rpcprotection"></a> Configuración de Hadoop.RPC.Protection

Una forma habitual de proteger la comunicación en un clúster de Hadoop consiste en cambiar la configuración de hadoop.rpc.protection a "Privacy" (Privacidad) o "Integrity" (Integridad). De forma predeterminada, PolyBase da por hecho que la configuración está establecida en "Autenticar". Para reemplazar esta configuración predeterminada, agregue la siguiente propiedad al archivo core-site.xml. Si cambia esta configuración, permitirá que se efectúe una transferencia de datos segura entre los nodos de Hadoop y que se establezca una conexión SSL con SQL Server.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a name="example-xml-files-for-cdh-5x-cluster"></a>Archivos XML de ejemplo para el clúster CDH 5.X

Yarn-site.xml con la configuración yarn.application.classpath y mapreduce.application.classpath.

```xml
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

Si decide dividir las dos opciones de configuración en mapred-site.xml y yarn-site.xml, los archivos sería el siguiente:

**yarn-site.xml**

```xml
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

Tenga en cuenta que hemos agregado la propiedad mapreduce.application.classpath. En CDH 5.x, encontrará los valores de configuración en la misma convención de nomenclatura en Ambari.

```xml
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

Tenga en cuenta que cuando PolyBase se autentica en un clúster protegido de Kerberos, espera que la configuración de hadoop.rpc.protection esté establecida en "Autenticar" de forma predeterminada. Esta acción dejará la comunicación de datos entre los nodos Hadoop sin cifrar. Para usar la configuración de "Privacidad" o "Integridad" para hadoop.rpc.protection, actualice el archivo core-site.xml en el servidor de PolyBase. Para más información, vea la sección anterior titulada [Conectarse al clúster de Hadoop con la opción de configuración Hadoop.RPC.Protection](#rpcprotection).

Para conectarse a un Hadoop protegido con Kerberos con MIT KDC se necesitan los siguientes cambios en todos los puntos de acceso de clúster de proceso nodos y el nodo de control:

1. Buscar los directorios de la configuración de Hadoop en la ruta de instalación de puntos de acceso. Normalmente, la ruta de acceso es:  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. Busque el valor de configuración del lado de Hadoop de las claves de configuración que se muestran en la tabla. (En el equipo de Hadoop, busque los archivos en el directorio de configuración de Hadoop).  
   
3. Copie los valores de configuración en la propiedad Value en los archivos correspondientes en el equipo de SQL Server.  
   
   |**#**|**Archivo de configuración**|**Clave de configuración**|**Acción**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|Especifique el nombre de host KDC. Por ejemplo: kerberos.su-dominio.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Especifique el dominio Kerberos. Por ejemplo: SU-DOMINIO.COM|  
   |3|core-site.xml|hadoop.security.authentication|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: KERBEROS<br></br>**Nota de seguridad:** KERBEROS debe estar en mayúsculas. Si aparece en minúsculas, puede que no esté activado.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: 10.193.26.174:10020|  
   |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. Cree un objeto de credencial con ámbito de base de datos para especificar la información de autenticación para cada usuario de Hadoop. Vea [PolyBase T-SQL objects (Objetos T-SQL de PolyBase)](../relational-databases/polybase/polybase-t-sql-objects.md).

## <a id="encryptionzone"></a> Programa de instalación de la zona de cifrado de Hadoop
Si usa Hadoop zona cifrado modificar core-site.xml y hdfs-site.xml como sigue. Proporcione la dirección ip que se ejecuta el servicio de KMS con el número de puerto correspondiente. El puerto predeterminado para KMS en CDH es 16 000.

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```