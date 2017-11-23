---
title: Configurar la conectividad de PolyBase para datos externos (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: "43"
ms.openlocfilehash: 7d486992f688b5bc914508ef000f23209b4bde89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-polybase-connectivity-to-external-data"></a>Configurar la conectividad de PolyBase para datos externos
Explica cómo configurar PolyBase en PDW de SQL Server para conectarse a Microsoft Azure o Hadoop almacenamiento blob orígenes de datos externos. Use PolyBase para ejecutar consultas que integran datos procedentes de varios orígenes, como Hadoop y almacenamiento de blobs de Azure, SQL Server PDW.  
  
### <a name="to-configure-connectivity"></a>Para configurar la conectividad  
  
1.  Abra una herramienta de consulta, como sqlcmd o SQL Server Data Tools (SSDT) y ejecuta sp_configure para ver la configuración actual de la "conectividad de hadoop".  
  
    ![configuración de conectividad de hadoop](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Decidir qué configuración necesario y si tiene que cambiar la configuración actual de conectividad de Hadoop. Esta opción se aplica a toda la región de PDW de SQL Server. Para obtener una lista completa de los valores de configuración y las versiones, vea [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
3.  Para cambiar la configuración de "conectividad de hadoop", ejecute sp_configure con RECONFIGURE. Estos son algunos ejemplos.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
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
  
    Ejecución de sp_configure con RECONFIGURE establece el valor de configuración. Reiniciar la región es necesario para establecer el valor de ejecución. Puesto que se requiere un reinicio después de la detención siguiente también, no es necesario realizar el reinicio hasta que después del siguiente paso que cambia core-site.xml.  
  
4.  Para habilitar el almacenamiento de blobs de Microsoft Azure como origen de datos externo, agregue uno o varios Microsoft Azure almacenamiento cuenta teclas de acceso al archivo de core-site.xml PDW. Para agregar una clave:  
  
    1.  Buscar el nombre de cuenta de almacenamiento de Microsoft Azure. Para ver las cuentas de almacenamiento, inicie sesión en el[portal de Azure](https://portal.azure.com) y haga clic en **cuentas de almacenamiento (clásica)**.  
  
        ![Nombre de cuenta de almacenamiento de Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Buscar la clave de acceso de la cuenta de almacenamiento de Azure. Para ello, haga clic en el nombre de cuenta de almacenamiento y, en la hoja de configuración, haga clic en **claves**. Esto le mostrará las claves de almacenamiento y el nombre de cuenta.  
  
        ![Claves de acceso de cuenta de almacenamiento de Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  Abra una conexión a escritorio remota al nodo de Control de PDW.  
  
    4.  Abra el archivo C:\Program Files\Microsoft SQL Server Parallel datos Warehouse\100\Hadoop\conf\core-site.xml.  
  
    5.  Agregue la siguiente propiedad con atributos de nombre y valor a core-site.xml.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        Este ejemplo utiliza la clave de acceso y nombre de cuenta que se ha mostrado anteriormente.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Tome medidas de seguridad antes de almacenar la clave de acceso en core-site.xml. Cualquier usuario que tenga el permiso CONTROL SERVER o ALTER ANY EXTERNAL DATA SOURCE puede crear un origen de datos externo que tiene acceso a esta cuenta. Una vez creado el origen de datos externo, todos los usuarios de PDW de SQL Server que tienen permiso para crear tablas pueden crear una tabla externa que tiene acceso a esta cuenta de almacenamiento. Los usuarios, a continuación, podrá tener acceso a datos de la cuenta y consume recursos de la cuenta.  
  
    6.  Guarde los cambios en core-site.xml.  
  
5.  Agregar propiedad yarn.application.classpath y los valores en el archivo yarn-site.xml.  
  
    Omita este paso si se está conectando a un 1.3 Hadoop externo.  
  
    A partir de Hadoop 2.0, el archivo de yarn-site.xml contiene valores de configuración para el marco de trabajo de Hadoop YARN. Este archivo se encuentra en el nodo de Control en **C:\program files\Microsoft Warehouse\100\Hadoop\conf paralelas de datos de SQL Server\\**.  
  
    Para ejecutar las consultas de PolyBase en un clúster de 2.0 externo de Hadoop en Windows o Linux, debe configurar la propiedad yarn.application.classpath y los valores para que sean coherentes con la configuración de yarn-site.xml en su Hadoop clúster externo. Esta configuración es necesaria incluso si el Hadoop clúster externo utiliza la configuración predeterminada.  
  
    Ejemplo de configuración predeterminado:  
  
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
  
    Una vez que una propiedad se define en yarn-site.xml, PolyBase utilizarán esos valores de propiedad cuando ejecuta consultas en la HDInsight región. Si planea ejecutar consultas de PolyBase en la HDInsight región y un clúster de 2.0 externo de Hadoop en Windows, debe haber coherencia entre todos los archivos de yarn-site.xml, o bien se producirá un error en las consultas de PolyBase.  
  
    Para ejecutar PolyBase en la HDInsight región y un clúster de 2.0 Hadoop externo, use la configuración predeterminada de yarn-site.xml en su Hadoop clúster externo.  
  
6.  Reinicie la región PDW. Para ello, use la herramienta Administrador de configuración. Vea [iniciar el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41; ](launch-the-configuration-manager.md).  
  
7.  Compruebe la configuración de seguridad para las conexiones de Hadoop. Si el **autenticación débil** en Hadoop lado se habilita mediante `dfs.permission = true`, debe crear un usuario de Hadoop **pdw_user** y conceda acceso completo de lectura y permisos de escritura para este usuario. PDW de SQL Server y las llamadas correspondientes de SQL Server PDW siempre se emiten como **pdw_user** que es un nombre de usuario fijo y no se puede cambiar en esta versión de conectividad de Hadoop y la versión de SQL Server PDW. Si se deshabilita la seguridad de Hadoop mediante el uso de `dfs.permission = false`, a continuación, es necesario realizar ninguna acción adicional.  
  
8.  Decidir qué usuarios pueden crear orígenes de datos externos para el almacenamiento de blobs de Microsoft Azure. Proporcionar a cada uno de estos usuarios, el nombre de cuenta de almacenamiento y también **ALTER ANY EXTERNAL DATA SOURCE** o **CONTROL SERVER** permiso.  
  
9. Para las conexiones de Hadoop, decidir qué usuarios pueden crear orígenes de datos externos en Hadoop. Proporcionar a cada uno de estos usuarios, el número de puerto y la dirección IP de cada nodo de nombre de Hadoop y asígneles **ALTER ANY EXTERNAL DATA SOURCE** o **CONTROL SERVER** permiso.  
  
10. Conectarse a WASB, también requiere el reenvío de DNS debe configurarse en el dispositivo. Para configurar el reenvío de DNS, consulte [usar un reenviador de DNS para resolver los nombres DNS no dispositivo &#40; Sistema de la plataforma de análisis &#41; ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
Los usuarios autorizados ahora pueden crear orígenes de datos externos, formatos de archivo externos y tablas externas. Pueden utilizar para integrar datos procedentes de varios orígenes como Hadoop, almacenamiento de blobs de Microsoft Azure y SQL Server PDW.  
  
## <a name="see-also"></a>Vea también  
[Configuración de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
