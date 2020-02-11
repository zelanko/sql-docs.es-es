---
title: Servidores vinculados (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8c2909eeebde268b52ecaeff5a20a982831e7569
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62743521"
---
# <a name="linked-servers-database-engine"></a>Servidores vinculados (motor de base de datos)
  Configure un servidor vinculado para habilitar a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para que ejecute comandos en orígenes de datos OLE DB fuera de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los servidores vinculados normalmente se configuran para habilitar [!INCLUDE[ssDE](../../includes/ssde-md.md)] a fin de ejecutar una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que incluye las tablas de otra instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]u otro producto de base de datos como Oracle. Muchos orígenes de datos OLE DB de tipos pueden configurarse como servidores vinculados, incluidos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access y Excel. Los servidores vinculados ofrecen las siguientes ventajas:  
  
-   Capacidad de obtener acceso a datos fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Capacidad de ejecutar consultas distribuidas, actualizaciones, comandos y transacciones en orígenes de datos heterogéneos en toda la organización.  
  
-   Capacidad de tratar diferentes orígenes de datos de manera similar.  
  
 Puede configurar un servidor vinculado con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o con la instrucción [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) . Los proveedores OLE DB varían en gran medida en el tipo y el número de parámetros necesarios. Por ejemplo, algunos proveedores requieren que proporcione un contexto de seguridad para la conexión con [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql). Algunos proveedores OLE DB que permiten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] actualizar datos en el origen de OLE DB. Otros solo proporcionan acceso a datos de solo lectura. Para obtener información acerca de cada proveedor OLE DB, consulte la documentación para dicho proveedor OLE DB.  
  
## <a name="linked-server-components"></a>Componentes de servidores vinculados  
 Una definición de servidor vinculado especifica los siguientes objetos:  
  
-   Un proveedor OLE DB  
  
-   Un origen de datos OLE DB  
  
 Un *proveedor OLE DB* es una biblioteca DLL que administra un origen de datos específico e interactúa con él. Un *origen de datos OLE DB* identifica la base datos específica a la que se puede tener acceso mediante OLE DB. Aunque los orígenes de datos en los que se realizan consultas a través de definiciones de servidores vinculados son bases de datos normales, existen proveedores OLE DB para una amplia variedad de archivos y formatos de archivo. Se trata de archivos de texto, datos de hojas de cálculo y los resultados de búsquedas de contenido de texto completo.  
  
 El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client (ProgID: SQLNCLI11) es el proveedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB oficial para.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] están diseñadas para ser usadas con cualquier proveedor OLE DB que implemente las interfaces OLE DB requeridas. Sin embargo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo se ha probado con el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y algunos otros.  
  
## <a name="linked-server-details"></a>Detalles de servidores vinculados  
 En la siguiente ilustración se muestran los conceptos básicos de una configuración con servidores vinculados.  
  
 ![Nivel de cliente, nivel de servidor y nivel de servidor de base de datos](../../database-engine/media/lsvr.gif "Nivel de cliente, nivel de servidor y nivel de servidor de base de datos")  
  
 Normalmente, los servidores vinculados se utilizan para tratar consultas distribuidas. Cuando una aplicación cliente ejecuta una consulta distribuida mediante un servidor vinculado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] analiza el comando y envía solicitudes a OLE DB. La solicitud de conjuntos de filas se puede realizar como una consulta al proveedor o abriendo una tabla base del proveedor.  
  
 Para que un origen de datos devuelva información mediante un servidor vinculado, el proveedor OLE DB (DLL) para ese origen de datos debe encontrarse en el mismo servidor que la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Cuando se utiliza un proveedor OLE DB de otro fabricante, la cuenta con la que se ejecuta el servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener permisos de lectura y ejecución para el directorio y todos los subdirectorios en los que esté instalado el proveedor.  
  
## <a name="managing-providers"></a>Administrar proveedores  
 Existe un conjunto de opciones para controlar cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] carga y utiliza proveedores OLE DB que se hayan especificado en el registro.  
  
## <a name="managing-linked-server-definitions"></a>Administrar definiciones de servidores vinculados  
 Cuando configure un servidor vinculado, registre la información de la conexión y del origen de datos con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Una vez realizado el registro, se puede hacer referencia a ese origen de datos con un único nombre lógico.  
  
 Puede utilizar procedimientos almacenados y vistas de catálogo para administrar definiciones de servidores vinculados:  
  
-   Cree una definición de servidor vinculado mediante la ejecución de **sp_addlinkedserver**.  
  
-   Vea información acerca de los servidores vinculados definidos en una instancia específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ejecutando una consulta en las vistas de catálogo del sistema **sys.servers** .  
  
-   Elimine una definición de servidor vinculado mediante la ejecución de **sp_dropserver**. También puede utilizar este procedimiento almacenado para quitar servidores remotos.  
  
 También puede definir servidores vinculados mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. En el Explorador de objetos, haga clic con el botón derecho en **Objetos de servidor**, seleccione **Nuevo**y, después, **Servidor vinculado**. Puede eliminar una definición de servidor vinculado al hacer clic con el botón derecho en el nombre del servidor vinculado y seleccionar **Eliminar**.  
  
 Cuando ejecute una consulta distribuida en un servidor vinculado, incluya el nombre de cuatro partes completo de una tabla para cada origen de datos en el que desee realizar la consulta. Este nombre de cuatro partes debe tener el formato _linked_server_name. Catalog_**_`schema`_..** _object_name_.  
  
> [!NOTE]  
>  Es posible definir servidores vinculados que señalen al servidor donde se han definido, es decir, que operen como bucle invertido. Los servidores en bucle invertido resultan muy útiles cuando se prueba una aplicación que utiliza consultas distribuidas en una red con un único servidor. Los servidores vinculados en bucle invertido están previstos para la realización de pruebas y no se admiten para muchas operaciones, como las transacciones distribuidas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Crear servidores vinculados &#40;SQL Server Motor de base de datos&#41;](create-linked-servers-sql-server-database-engine.md)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_dropserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropserver-transact-sql)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Sys. Servers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql)  
  
 [sp_linkedservers &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)  
  
  
