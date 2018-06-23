---
title: Almacenamiento en caché de plantillas, XSL y esquemas (SQLXML 4.0) | Documentos de Microsoft
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
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5a1108e32f807345320745c9f791a558ecf07caa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113994"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Almacenar en memoria caché plantillas, XSL y esquemas (SQLXML 4.0)
  Para mejorar el rendimiento, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 permite almacenar en la memoria caché plantillas, archivos XSL y esquemas.  
  
 Todos los esquemas, plantillas y archivos XSL (excepto los archivos de una ubicación http:// o ftp://) están almacenados en la memoria caché. Los archivos almacenados en la memoria caché permanecen en memoria mientras el proceso se está ejecutando. Cuando finaliza el proceso, se pierde toda la caché. Por consiguiente, si ejecuta un proceso por consulta, es posible que no se aprecien las ventajas del almacenamiento en caché.  
  
 Los temas de esta sección proporcionan más información sobre cómo almacenar en memoria caché.  
  
## <a name="in-this-section"></a>En esta sección  
 [Almacenamiento en caché de plantilla &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)  
 Se describe y proporciona una clave del Registro para el almacenamiento en caché de las plantillas.  
  
 [Almacenamiento en caché XSL &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
 Se describe y proporciona una clave del Registro para el almacenamiento en caché de archivos XSL.  
  
 [Almacenamiento en caché de esquema &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
 Se explican cuestiones de instalación simultánea de SQLXML relacionadas con el almacenamiento en la memoria caché de esquemas y proporciona las claves del Registro para el almacenamiento en caché de esquemas.  
  
  