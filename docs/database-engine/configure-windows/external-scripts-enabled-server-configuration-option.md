---
title: "Opci&#243;n de configuraci&#243;n de servidor Scripts externos habilitados | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
f1_keywords: 
  - "external scripts enabled"
  - "external_scripts_enabled_TSQL"
helpviewer_keywords: 
  - "opción scripts externos habilitados"
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Opci&#243;n de configuraci&#243;n de servidor Scripts externos habilitados
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **external scripts enabled** para habilitar la ejecución de scripts con determinadas extensiones de lenguaje remoto. Esta propiedad será OFF de forma predeterminada. El programa de instalación, opcionalmente, puede establecer esta propiedad en true si **Advanced Analytics Services** (Servicios de análisis avanzado) está instalado.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658).|  
  
 Debe habilitar la opción de script externo habilitado antes de poder ejecutar un script externo mediante el procedimiento **sp_execute_external_script**. Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible, como R. En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un componente de servidor instalado con [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], y un conjunto de herramientas de estación de trabajo y bibliotecas de conectividad que conectan a los científicos de datos al entorno de alto rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Instale la característica **Extensiones de análisis avanzado** durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar la ejecución de los scripts de R. Para obtener más información, consulte [Installing Previous Versions of SQL Server R Services](../Topic/Installing%20Previous%20Versions%20of%20SQL%20Server%20R%20Services.md).  
  
 Ejecute el script siguiente para habilitar los scripts externos.  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE;  
```  
  
 Debe reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que este cambio surta efecto.  
  
## Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  