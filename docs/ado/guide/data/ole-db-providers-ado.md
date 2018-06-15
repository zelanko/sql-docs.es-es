---
title: Proveedores OLE DB (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae1cb60ac963b71814cfc225e42799c375081e5b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272164"
---
# <a name="ole-db-providers-ado"></a>Proveedores OLE DB (ADO)
OLE DB define un conjunto de interfaces COM para proporcionar a las aplicaciones acceso uniforme a los datos almacenados en diversos orígenes de información. Este enfoque permite a un origen de datos compartir sus datos a través de las interfaces que admiten la cantidad de la funcionalidad DBMS adecuada para el origen de datos. De forma predeterminada, la arquitectura de alto rendimiento de OLE DB se basa en el uso de un modelo de servicios flexible basado en componentes. En lugar de tener un número predefinido de capas intermedias entre la aplicación y los datos, OLE DB sólo requiere muchos componentes que son necesarios para realización una tarea determinada.  
  
 Por ejemplo, suponga que un usuario desea volver a ejecutar una consulta. Considere los casos siguientes:  
  
-   Los datos residen en una base de datos relacional para la que existe actualmente un controlador ODBC, pero ningún proveedor OLE DB nativo: la aplicación utiliza ADO para comunicarse con el proveedor OLE DB para ODBC, que, a continuación, carga el controlador ODBC adecuado. El controlador pasa la instrucción SQL en el DBMS, que recupera los datos.  
  
-   Los datos residen en Microsoft SQL Server para el que existe un proveedor OLE DB nativo: la aplicación utiliza ADO para comunicarse directamente con el proveedor OLE DB para Microsoft SQL Server. Se necesita ningún intermediario.  
  
-   Los datos residen en Microsoft Exchange Server, para lo que hay un proveedor OLE DB, pero que no expone un motor para procesar las consultas SQL: la aplicación utiliza ADO para comunicarse con el proveedor OLE DB para Microsoft Exchange y llama a un procesador de consultas de OLE DB componente para procesar las consultas.  
  
-   Los datos residen en el sistema de archivos NTFS de Microsoft en forma de documentos: acceso a los datos mediante el uso de un proveedor OLE DB nativo a través de servicios de Index Server de Microsoft, que indiza el contenido y las propiedades de documentos en el sistema de archivos para habilitar el contenido eficaz realiza una búsqueda.  
  
 En todos los ejemplos anteriores, la aplicación puede consultar los datos. Se cumplen las necesidades del usuario con un número mínimo de componentes. En cada caso, se utilizan componentes adicionales solo si es necesario y se invocan únicamente los componentes necesarios. Esta carga a petición de componentes reutilizables y pueden compartirse en gran medida contribuye a alto rendimiento cuando se utiliza OLE DB.  
  
 Los proveedores se dividen en dos categorías: aquellos que proporcionan datos y aquellos que proporcionan servicios. Un proveedor de datos tiene sus propios datos y expone en formato tabular en su aplicación. Un proveedor de servicios encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Un proveedor de servicios también puede definirse como un componente de servicio, que debe funcionar conjuntamente con otros componentes o proveedores de servicios.  
  
 ADO proporciona coherente, la interfaz de nivel superior para los distintos proveedores de OLE DB.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Proveedores de datos](../../../ado/guide/data/data-providers.md)  
  
-   [Proveedores de servicios y componentes](../../../ado/guide/data/service-providers-and-components.md)
