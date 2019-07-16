---
title: Proveedores OLE DB (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e86375639d875f5cfec21705af47c005afd901e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924756"
---
# <a name="ole-db-providers-ado"></a>Proveedores OLE DB (ADO)
OLE DB define un conjunto de interfaces COM para proporcionar a las aplicaciones acceso uniforme a los datos almacenados en diversos orígenes de información. Este enfoque permite a un origen de datos compartir sus datos a través de las interfaces que admiten la cantidad de funcionalidad del DBMS correspondiente al origen de datos. Por diseño, la arquitectura de alto rendimiento de OLE DB se basa en el uso de un modelo flexible y basado en componentes de servicios. En lugar de tener un número predefinido de capas intermedias entre la aplicación y los datos, OLE DB sólo requiere muchos componentes que son necesarios para realización una tarea determinada.  
  
 Por ejemplo, suponga que un usuario desea ejecutar una consulta. Considere los casos siguientes:  
  
-   Los datos residen en una base de datos relacional para el que existe actualmente un controlador ODBC, pero ningún proveedor OLE DB nativo: La aplicación utiliza ADO para comunicarse con el proveedor OLE DB para ODBC, que, a continuación, carga el controlador ODBC adecuado. El controlador pasa la instrucción SQL para el DBMS, que recupera los datos.  
  
-   Los datos residen en Microsoft SQL Server para el que existe un proveedor OLE DB nativo: La aplicación utiliza ADO para comunicarse directamente con el proveedor OLE DB para Microsoft SQL Server. Se necesita ningún intermediario.  
  
-   Los datos residen en Microsoft Exchange Server, para lo que hay un proveedor OLE DB, pero que no expone un motor para procesar consultas SQL: La aplicación utiliza ADO para comunicarse con el proveedor OLE DB para Microsoft Exchange y llama a un componente de procesador de consultas de OLE DB para procesar las consultas.  
  
-   Los datos residen en el sistema de archivos NTFS de Microsoft en forma de documentos: Se tiene acceso a datos mediante un proveedor OLE DB nativo a través de servicios de Index Server de Microsoft, que indiza el contenido y propiedades de los documentos en el sistema de archivos para habilitar búsquedas eficaces con contenido.  
  
 En todos los ejemplos anteriores, la aplicación puede consultar los datos. Se cumplen las necesidades del usuario con un número mínimo de componentes. En cada caso, se usan componentes adicionales solo si es necesario y se invocan únicamente los componentes necesarios. Esta carga de petición de componentes reutilizables y que se pueda compartir contribuye en gran medida a alto rendimiento cuando se utiliza OLE DB.  
  
 Los proveedores se dividen en dos categorías: aquellos que proporcionan datos y aquellos que proporcionan servicios. Un proveedor de datos tiene sus propios datos y expone en un formato tabular en la aplicación. Un proveedor de servicios encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Un proveedor de servicios también puede definirse como un componente de servicio, que debe trabajar conjuntamente con otros proveedores de servicios o componentes.  
  
 ADO ofrece una coherente interfaz de nivel superior para los distintos proveedores de OLE DB.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Proveedores de datos](../../../ado/guide/data/data-providers.md)  
  
-   [Proveedores de servicios y componentes](../../../ado/guide/data/service-providers-and-components.md)
