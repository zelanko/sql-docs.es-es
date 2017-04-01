---
title: "Configuraci&#243;n de PolyBase | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 12
---
# Configuraci&#243;n de PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Utilice los procedimientos siguientes para configurar PolyBase.  
  
## <a name="external-data-source-configuration"></a>Configuración del origen de datos externo  
 Debe asegurarse de que funciona correctamente la conectividad desde SQL Server al origen de datos externo. El tipo de conectividad influye significativamente en el rendimiento esperado de las consultas. Por ejemplo, un vínculo de 10 Gigabit Ethernet producirá un tiempo de respuesta de consulta menor en las consultas PolyBase que uno de 1 Gigabit Ethernet.  
  
 Debe configurar SQL Server para conectarse a la versión de Hadoop o a Almacenamiento de blobs de Azure con **sp_configure**. PolyBase es compatible con dos distribuciones de Hadoop: Hortonworks Data Platform (HDP) y Cloudera Distributed Hadoop (CDH).  Para obtener una lista completa de los orígenes de datos externos compatibles, vea [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
### <a name="run-spconfigure"></a>Ejecución de sp_configure  
  
1.  Ejecute la “conectividad de hadoop” sp_configure y defina un valor adecuado.  Para hallar el valor, vea [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
    ```tsql  
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
 Para mejorar el rendimiento de las consultas, habilite el cálculo de la aplicación para un clúster de Hadoop:  
  
1.  Busque el archivo **yarn-site.xml** en la ruta de acceso de instalación de SQL Server. Normalmente, la ruta de acceso es:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  En el equipo de Hadoop, busque el archivo análogo en el directorio de configuración de Hadoop. En el archivo, busque y copie el valor de la clave de configuración yarn.application.classpath.  
  
3.  En el equipo de SQL Server, en el **archivo yarn.site.xml,** busque la propiedad **yarn.application.classpath** . Pegue el valor de la máquina de Hadoop en el elemento de valor.  
  
## <a name="kerberos-configuration"></a>Configuración de Kerberos  
 Para conectarse a un clúster de Hadoop protegido con Kerberos [con MIT KDC]:  
  
1.  Busque el directorio de configuración de Hadoop en la ruta de acceso de instalación de SQL Server. Normalmente, la ruta de acceso es:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Busque el valor de configuración del lado de Hadoop de las claves de configuración que se muestran en la tabla. (En el equipo de Hadoop, busque los archivos en el directorio de configuración de Hadoop).  
  
3.  Copie los valores de configuración en la propiedad Value en los archivos correspondientes en el equipo de SQL Server.  
  
    |**#**|**Archivo de configuración**|**Clave de configuración**|**Acción**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique el dominio Kerberos. Por ejemplo: SU-DOMINIO.COM|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique el nombre de host KDC. Por ejemplo: kerberos.su-dominio.com.|  
    |3|core-site.xml|hadoop.security.authentication|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: KERBEROS<br></br>**Nota de seguridad:** KERBEROS debe estar en mayúsculas. Si aparece en minúsculas, puede que no esté activado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.address|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, yarn/_HOST@YOUR-REALM.COM|  
  
4.  Cree un objeto de credencial con ámbito de base de datos para especificar la información de autenticación para cada usuario de Hadoop. Vea [PolyBase T-SQL objects (Objetos T-SQL de PolyBase)](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Objetos T-SQL de PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Vea también  
 [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  