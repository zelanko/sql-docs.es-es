---
title: Proveedores de datos | Documentos de Microsoft
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
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26f220f166e2269e59665a64c6e69504f298c5a9
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270704"
---
# <a name="data-providers"></a>Proveedores de datos
Proveedores de datos representan diversos orígenes de datos, como bases de datos SQL, archivos secuenciales indizados, hojas de cálculo, almacenes de documentos y archivos de correo electrónico. Los proveedores exponen datos uniformemente mediante una abstracción común que se denomina conjunto de filas.  
  
 ADO es eficaz y flexible porque puede conectarse a cualquiera de varios proveedores de datos y seguir exponiendo el mismo modelo de programación, sin tener en cuenta las características específicas de un proveedor determinado. Sin embargo, dado que cada proveedor de datos es único, cómo interactúa la aplicación con ADO variará por el proveedor de datos.  
  
 Por ejemplo, las capacidades y características del proveedor OLE DB para SQL Server, que se utiliza para tener acceso a las bases de datos de Microsoft SQL Server, son considerablemente diferentes de los del proveedor Microsoft OLE DB para la publicación en Internet, que se utiliza para tener acceso a archivos almacena en un servidor Web.
