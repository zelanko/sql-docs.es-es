---
title: Proveedores de datos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c92245f0504d5531235c5e5a33f8bf5b04362b10
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-providers"></a>Proveedores de datos
Proveedores de datos representan diversos orígenes de datos, como bases de datos SQL, archivos secuenciales indizados, hojas de cálculo, almacenes de documentos y archivos de correo electrónico. Los proveedores exponen datos uniformemente mediante una abstracción común que se denomina conjunto de filas.  
  
 ADO es eficaz y flexible porque puede conectarse a cualquiera de varios proveedores de datos y seguir exponiendo el mismo modelo de programación, sin tener en cuenta las características específicas de un proveedor determinado. Sin embargo, dado que cada proveedor de datos es único, cómo interactúa la aplicación con ADO variará por el proveedor de datos.  
  
 Por ejemplo, las capacidades y características del proveedor OLE DB para SQL Server, que se utiliza para tener acceso a las bases de datos de Microsoft SQL Server, son considerablemente diferentes de los del proveedor Microsoft OLE DB para la publicación en Internet, que se utiliza para tener acceso a archivos almacena en un servidor Web.
