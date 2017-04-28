---
title: Servidores vinculados (motor de base de datos) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB, linked servers
- OLE DB provider, linked servers
- server management [SQL Server], linked servers
- linked servers [SQL Server]
- distributed queries [SQL Server], linked servers
- servers [SQL Server], linked
- remote servers [SQL Server], linked servers
- linked servers [SQL Server], about linked servers
ms.assetid: 6ef578bf-8da7-46e0-88b5-e310fc908bb0
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0478ab684ec88babe308e30fd718f628b865dd7b
ms.lasthandoff: 04/11/2017

---
# <a name="linked-servers-database-engine"></a>Servidores vinculados (motor de base de datos)
  Configure un servidor vinculado para habilitar a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para que ejecute comandos en orígenes de datos OLE DB fuera de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los servidores vinculados normalmente se configuran para habilitar [!INCLUDE[ssDE](../../includes/ssde-md.md)] a fin de ejecutar una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que incluye las tablas de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]u otro producto de base de datos como Oracle. Muchos orígenes de datos OLE DB de tipos pueden configurarse como servidores vinculados, incluidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access y Excel. Los servidores vinculados ofrecen las siguientes ventajas:  
  
-   Capacidad de obtener acceso a datos fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Capacidad de ejecutar consultas distribuidas, actualizaciones, comandos y transacciones en orígenes de datos heterogéneos en toda la organización.  
  
-   Capacidad de tratar diferentes orígenes de datos de manera similar.  
  
 Puede configurar un servidor vinculado con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o con la instrucción [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) . Los proveedores OLE DB varían en gran medida en el tipo y el número de parámetros necesarios. Por ejemplo, algunos proveedores requieren que proporcione un contexto de seguridad para la conexión con [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md). Algunos proveedores OLE DB que permiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actualizar datos en el origen de OLE DB. Otros solo proporcionan acceso a datos de solo lectura. Para obtener información acerca de cada proveedor OLE DB, consulte la documentación para dicho proveedor OLE DB.  
  
## <a name="linked-server-components"></a>Componentes de servidores vinculados  
 Una definición de servidor vinculado especifica los siguientes objetos:  
  
-   Un proveedor OLE DB  
  
-   Un origen de datos OLE DB  
  
 Un *proveedor OLE DB* es una biblioteca DLL que administra un origen de datos específico e interactúa con él. Un *origen de datos OLE DB* identifica la base datos específica a la que se puede tener acceso mediante OLE DB. Aunque los orígenes de datos en los que se realizan consultas a través de definiciones de servidores vinculados son bases de datos normales, existen proveedores OLE DB para una amplia variedad de archivos y formatos de archivo. Se trata de archivos de texto, datos de hojas de cálculo y los resultados de búsquedas de contenido de texto completo.  
  
 El proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (PROGID: SQLNCLI11) es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están diseñadas para ser usadas con cualquier proveedor OLE DB que implemente las interfaces OLE DB requeridas. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo se ha probado con el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y algunos otros.  
  
## <a name="linked-server-details"></a>Detalles de servidores vinculados  
 En la siguiente ilustración se muestran los conceptos básicos de una configuración con servidores vinculados.  
  
 ![Nivel de cliente, nivel de servidor y nivel de servidor de base de datos](../../relational-databases/linked-servers/media/lsvr.gif "Nivel de cliente, nivel de servidor y nivel de servidor de base de datos")  
  
 Normalmente, los servidores vinculados se utilizan para tratar consultas distribuidas. Cuando una aplicación cliente ejecuta una consulta distribuida mediante un servidor vinculado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analiza el comando y envía solicitudes a OLE DB. La solicitud de conjuntos de filas se puede realizar como una consulta al proveedor o abriendo una tabla base del proveedor.  
  
 Para que un origen de datos devuelva información mediante un servidor vinculado, el proveedor OLE DB (DLL) para ese origen de datos debe encontrarse en el mismo servidor que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se utiliza un proveedor OLE DB de otro fabricante, la cuenta con la que se ejecuta el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de lectura y ejecución para el directorio y todos los subdirectorios en los que esté instalado el proveedor.  
  
## <a name="managing-providers"></a>Administrar proveedores  
 Existe un conjunto de opciones para controlar cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga y utiliza proveedores OLE DB que se hayan especificado en el registro.  
  
## <a name="managing-linked-server-definitions"></a>Administrar definiciones de servidores vinculados  
 Cuando configure un servidor vinculado, registre la información de la conexión y del origen de datos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una vez realizado el registro, se puede hacer referencia a ese origen de datos con un único nombre lógico.  
  
 Puede utilizar procedimientos almacenados y vistas de catálogo para administrar definiciones de servidores vinculados:  
  
-   Cree una definición de servidor vinculado mediante la ejecución de **sp_addlinkedserver**.  
  
-   Vea información acerca de los servidores vinculados definidos en una instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutando una consulta en las vistas de catálogo del sistema **sys.servers** .  
  
-   Elimine una definición de servidor vinculado mediante la ejecución de **sp_dropserver**. También puede utilizar este procedimiento almacenado para quitar servidores remotos.  
  
 También puede definir servidores vinculados mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. En el Explorador de objetos, haga clic con el botón derecho en **Objetos de servidor**, seleccione **Nuevo**y, después, **Servidor vinculado**. Puede eliminar una definición de servidor vinculado al hacer clic con el botón derecho en el nombre del servidor vinculado y seleccionar **Eliminar**.  
  
 Cuando ejecute una consulta distribuida en un servidor vinculado, incluya el nombre de cuatro partes completo de una tabla para cada origen de datos en el que desee realizar la consulta. Este nombre de cuatro partes debe tener el formato *linked_server_name.catalog***.***schema***.***object_name*.  
  
> [!NOTE]  
>  Es posible definir servidores vinculados que señalen al servidor donde se han definido, es decir, que operen como bucle invertido. Los servidores en bucle invertido resultan muy útiles cuando se prueba una aplicación que utiliza consultas distribuidas en una red con un único servidor. Los servidores vinculados en bucle invertido están previstos para la realización de pruebas y no se admiten para muchas operaciones, como las transacciones distribuidas.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Crear servidores vinculados &#40;Motor de base de datos de SQL Server&#41;](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [sys.servers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md)  
  
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)  
  
  
