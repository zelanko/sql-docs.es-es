---
title: Arquitectura de cliente y servidor XML formato (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 589ca305ee7fe492dd5342ab184b37abcfb5d2ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106919"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>Arquitectura de aplicación de formato XML en el cliente y en el servidor (SQLXML 4.0)
  La ilustración siguiente muestra la arquitectura del formato XML en el lado servidor.  
  
 ![Arquitectura de formato XML en el servidor. ] (../../../database-engine/dev-guide/media/serversidexml.gif "Formato arquitectura de XML en el lado del servidor.")  
  
 En este ejemplo, el comando que se especifica en el cliente se envía al servidor. El servidor genera un documento XML y lo devuelve al cliente. En este caso, el servidor tiene una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Con el formato XML del lado servidor, puede utilizar el proveedor SQLXMLOLEDB o el proveedor SQLOLEDB.  El proveedor SQLXMLOLEDB utiliza Sqlxml4.dll, incluido en SQLXML 4.0. Al utilizar el proveedor SQLOLEDB, de forma predeterminada obtiene la funcionalidad SQLXML que proporciona Sqlxmlx.dll, incluida con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows o en Microsoft Data Access Components (MDAC) 2.6 o posterior. Para utilizar Sqlxml4.dll con SQLOLEDB, debe establecer la propiedad de versión de SQLXML en "SQLXML.4.0" en el objeto de conexión de SQLOLEDB. En cualquier caso, el servidor genera el documento XML y lo envía al cliente.  
  
> [!NOTE]  
>  Los diagramas de actualización y las consultas XPath se analizan en el cliente. Para obtener la plantilla XPath o la funcionalidad de diagrama de actualización en SQLXML 4.0, utilice Sqlxml4.dll.  
  
 La ilustración siguiente muestra la arquitectura del formato XML del lado cliente.  
  
 ![Arquitectura de formato XML en el lado del cliente. ] (../../../database-engine/dev-guide/media/clientsidexml.gif "Formato arquitectura de XML en el lado del cliente.")  
  
 En este ejemplo, el cliente utiliza el proveedor SQLXMLOLEDB. En la cadena de conexión, la propiedad de proveedor de datos debe establecerse en SQLOLEDB. (Éste es el único valor aceptado en SQLXML 4.0.) El comando que se ejecuta en el cliente se envía al servidor. El conjunto de filas que se genera en el servidor se envía al cliente. En el cliente se lleva a cabo el formato del documento XML a partir del conjunto de filas.  
  
 En SQLXML 4.0, se pueden utilizar como proveedores de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) o el proveedor SQLOLEDB. Puede tener acceso a cualquier origen de datos. La transformación XML se puede aplicar en el cliente siempre que la consulta devuelva un único conjunto de filas.  
  
  