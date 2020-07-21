---
title: Proveedores de datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: rothja
ms.author: jroth
ms.openlocfilehash: 6dfb672b57b95224cf6ff056c3298c7c8a437d2a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761111"
---
# <a name="data-providers"></a>Proveedores de datos
Los proveedores de datos representan diversos orígenes de datos, como bases de datos SQL, archivos secuenciales indexados, hojas de cálculo, almacenes de documentos y archivos de correo. Los proveedores exponen datos uniformemente mediante una abstracción común denominada conjunto de filas.  
  
 ADO es eficaz y flexible porque puede conectarse a cualquiera de los distintos proveedores de datos y seguir exponiendo el mismo modelo de programación, independientemente de las características específicas de cualquier proveedor determinado. Sin embargo, dado que cada proveedor de datos es único, el modo en que la aplicación interactúa con ADO variará según el proveedor de datos.  
  
 Por ejemplo, las capacidades y características del proveedor de OLE DB para SQL Server, que se usa para tener acceso a las bases de datos de Microsoft SQL Server, son considerablemente diferentes de las de la publicación proveedor de Microsoft OLE DB para la publicación en Internet, que se usa para tener acceso a los almacenes de archivos en un servidor Web.
