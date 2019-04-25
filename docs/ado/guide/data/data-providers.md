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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c3b8a4ac0da80303a63bd62f7b4d6f51faab1fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472572"
---
# <a name="data-providers"></a>Proveedores de datos
Proveedores de datos representan diversos orígenes de datos, como las bases de datos SQL, archivos secuenciales indizados, hojas de cálculo, almacenes de documentos y archivos de correo. Los proveedores exponen datos uniformemente mediante una abstracción común denominada el conjunto de filas.  
  
 ADO es eficaz y flexible ya que puede conectarse a cualquiera de varios proveedores de datos y exponer sigue el modelo de programación mismo, independientemente de las características específicas de un proveedor determinado. Sin embargo, dado que cada proveedor de datos es único, cómo interactúa la aplicación con ADO variará por el proveedor de datos.  
  
 Por ejemplo, las funcionalidades y características del proveedor OLE DB para SQL Server, que se utiliza para tener acceso a las bases de datos de Microsoft SQL Server, son considerablemente diferentes de los que el proveedor Microsoft OLE DB para la publicación en Internet, que se usa para tener acceso a archivo almacena en un servidor Web.
