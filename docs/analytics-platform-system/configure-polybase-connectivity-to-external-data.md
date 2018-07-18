---
title: Configurar la conectividad de PolyBase - Analytics Platform System | Microsoft Docs
description: Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop o Microsoft Azure storage blob orígenes de datos externos. Uso de PolyBase para ejecutar consultas que se integran datos desde varios orígenes, como Hadoop, Azure blob storage y almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 26eeffb1d2a27ee49f01114b015ab4051b145d64
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909875"
---
# <a name="configure-polybase-connectivity-to-external-data"></a>Configurar la conectividad de PolyBase para datos externos
Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop o Microsoft Azure storage blob orígenes de datos externos. Uso de PolyBase para ejecutar consultas que se integran datos desde varios orígenes, como Hadoop, Azure blob storage y almacenamiento de datos paralelos.  
  
### <a name="to-configure-connectivity"></a>Para configurar la conectividad  
  
1.  Abra una herramienta de consulta, como sqlcmd o SQL Server Data Tools (SSDT) y ejecuta sp_configure para ver la configuración actual de 'hadoop connectivity'.  
  
    ![configuración de conectividad de hadoop](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Decidir qué configuración necesidad y si es preciso cambiar la configuración actual de conectividad de Hadoop. Esta opción se aplica a toda la región de PDW de SQL Server. Para obtener una lista completa de las opciones de configuración y las versiones, vea [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
3.  Para cambiar la configuración de 'hadoop connectivity', ejecute sp_configure con RECONFIGURE. Estos son algunos ejemplos.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP) or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    Ejecución de sp_configure con RECONFIGURE establece el valor de configuración. Reinicio de la región es necesario para establecer el valor de ejecución. Puesto que se requiere un reinicio después de la siguiente parada también, no es necesario realizar el reinicio hasta el paso siguiente, que cambia el archivo core-site.xml.  
  
4.  Para habilitar el almacenamiento de blobs de Microsoft Azure como origen de datos externo, agregue uno o varios Microsoft Azure storage cuenta teclas de acceso al archivo core-site.xml PDW. Para agregar una clave:  
  
    1.  Busque el nombre de cuenta de almacenamiento de Microsoft Azure. Para ver las cuentas de almacenamiento, inicie sesión en el[portal Azure](https://portal.azure.com) y haga clic en **cuentas de almacenamiento (clásico)**.  
  
        ![Nombre de cuenta de almacenamiento de Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Busque la clave de acceso de la cuenta de almacenamiento de Azure. Para ello, haga clic en el nombre de cuenta de almacenamiento y, en la hoja configuración, haga clic en **claves**. Esto muestra las claves de almacenamiento y el nombre de cuenta.  
  
        ![Claves de acceso de cuenta de almacenamiento de Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  Abra una conexión a escritorio remota al nodo de Control de PDW.  
  
    4.  Abra el archivo C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\core-site.xml.  
  
    5.  Agregue la siguiente propiedad con atributos de nombre y valor a core-site.xml.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        Este ejemplo utiliza la clave de acceso y el nombre de cuenta que se mostró anteriormente.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Tome medidas de seguridad antes de almacenar la clave de acceso en core-site.xml. Cualquier usuario que tenga el permiso CONTROL SERVER o ALTER ANY EXTERNAL DATA SOURCE puede crear un origen de datos externo que tiene acceso a esta cuenta. Una vez creado el origen de datos externo, todos los usuarios de PDW de SQL Server con los permisos CREATE TABLE pueden crear una tabla externa que tenga acceso a esta cuenta de almacenamiento. Los usuarios pueden tener acceso a datos de la cuenta y consumir recursos de la cuenta.  
  
    6.  Guarde los cambios en core-site.xml.  
  
5.  Agregar propiedad yarn.application.classpath y los valores para el archivo yarn-site.xml.  
  
    Omita este paso si se conecta a un 1.3 externo de Hadoop.  
  
    A partir de Hadoop 2.0, el archivo yarn-site.xml contiene opciones de configuración para el marco de trabajo de YARN de Hadoop. Este archivo se encuentra en el nodo de Control en **C:\program files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\\**.  
  
    Para ejecutar las consultas de PolyBase en un clúster externo de Hadoop 2.0 en Windows o Linux, deberá configurar la propiedad yarn.application.classpath y los valores sean coherentes con la configuración de yarn-site.xml en el Hadoop clúster externo. Esta configuración es necesaria incluso si el Hadoop clúster externo usa la configuración predeterminada.  
  
    Ejemplo de configuración predeterminada:  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    Una vez que cualquier propiedad se define en yarn-site.xml, PolyBase usa esos valores de propiedad cuando ejecuta consultas en Hadoop. Si planea ejecutar consultas de PolyBase en Azure Blob Storage y un clúster externo de Hadoop 2.0 en Windows, debe haber coherencia entre todos los archivos yarn-site.xml, o bien se producirá un error en las consultas de PolyBase.  
   
6.  Reinicie la región PDW. Para ello, use la herramienta Administrador de configuración. Consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
7.  Compruebe la configuración de seguridad para las conexiones de Hadoop. Si el **autenticación débil** en Hadoop lado se habilita mediante `dfs.permission = true`, debe crear un usuario de Hadoop **pdw_user** y conceda acceso completo de lectura y permisos de escritura para este usuario. PDW de SQL Server y las llamadas correspondientes de PDW de SQL Server siempre se emiten como **pdw_user**.  Esto es un nombre de usuario fijo y no se puede cambiar en esta versión de la conectividad de Hadoop y la versión de PDW de SQL Server. Si se deshabilita la seguridad de Hadoop mediante el uso de `dfs.permission = false`, a continuación, es necesario realizar ninguna acción adicional.  
  
8.  Decidir qué usuarios pueden crear un origen de datos externo para el almacenamiento de blobs de Microsoft Azure. Asigne a cada uno de estos usuarios, el nombre de cuenta de almacenamiento y también **ALTER ANY EXTERNAL DATA SOURCE** o **CONTROL SERVER** permiso.  
  
9. Para las conexiones de Hadoop, decidir qué usuarios pueden crear un origen de datos externos en Hadoop. Asigne a cada uno de estos usuarios, el número de puerto y la dirección IP de cada nodo de nombre de Hadoop y asígneles **ALTER ANY EXTERNAL DATA SOURCE** o **CONTROL SERVER** permiso.  
  
10. Conectarse a WASB, también requiere el reenvío de DNS que se configurará en el dispositivo. Para configurar el reenvío de DNS, consulte [usar un reenviador DNS para resolver los nombres DNS que no son de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
Los usuarios autorizados ahora pueden crear orígenes de datos externos, formatos de archivo externos y tablas externas. Puede usarlas para integrar datos de varios orígenes, como Hadoop, Microsoft Azure blob storage y SQL Server PDW.  

## <a name="kerberos-configuration"></a>Configuración de Kerberos  
Tenga en cuenta que cuando PolyBase se autentica en un clúster protegido de Kerberos, debe establecer la configuración de hadoop.rpc.protection para la autenticación. Esta acción dejará la comunicación de datos entre los nodos Hadoop sin cifrar. 

 Para conectarse a un clúster de Hadoop protegido con Kerberos [con MIT KDC]:
   
  
1.  Busque el directorio de configuración de Hadoop en la ruta de instalación en el nodo de Control:  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  Busque el valor de configuración del lado de Hadoop de las claves de configuración que se muestran en la tabla. (En el equipo de Hadoop, busque los archivos en el directorio de configuración de Hadoop).  
  
3.  Copie los valores de configuración en la propiedad value en los archivos correspondientes en el nodo de Control.  
  
    |**#**|**Archivo de configuración**|**Clave de configuración**|**Acción**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique el nombre de host KDC. Por ejemplo: kerberos.su-dominio.com.|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique el dominio Kerberos. Por ejemplo: SU-DOMINIO.COM|  
    |3|core-site.xml|hadoop.security.authentication|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: KERBEROS<br></br>**Nota de seguridad:** KERBEROS debe estar en mayúsculas. Si aparece en minúsculas, puede que no esté activado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, yarn/_HOST@YOUR-REALM.COM|  
  
4. Cree un objeto de credencial con ámbito de base de datos para especificar la información de autenticación para cada usuario de Hadoop. Vea [PolyBase T-SQL objects (Objetos T-SQL de PolyBase)](../relational-databases/polybase/polybase-t-sql-objects.md).  

5. Reinicie la región PDW. Para ello, use la herramienta Administrador de configuración. Consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).
 
## <a name="see-also"></a>Vea también  
[Configuración de dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
