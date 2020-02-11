---
title: Mensajes de error de ODBC jet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915813"
---
# <a name="odbc-jet-error-messages"></a>Mensajes de Error de Jet de ODBC
En el caso de los errores que se producen en el origen de datos, el controlador ODBC devuelve un mensaje de error devuelto por la biblioteca de archivos ODBC. En el caso de los errores que se producen en el controlador ODBC o en el administrador de controladores, el controlador devuelve un mensaje de error basado en el texto asociado al SQLSTATE.  
  
 Los mensajes de error tienen el siguiente formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Los prefijos entre corchetes ([]) identifican la ubicación del error. Cuando el error se produce en el administrador de controladores, no se proporciona el *origen de datos* . Cuando el error se produce en el origen de datos, los prefijos [*Vendor*] y [*ODBC-Component*] identifican el proveedor y el nombre del componente ODBC que recibió el error del origen de datos.  
  
 En la tabla siguiente se muestran los mensajes de error devueltos por el administrador de controladores y el ISAM del controlador:  
  
|Mensaje de error|Ubicación del error|  
|-------------------|--------------------|  
|Microsoft [Administrador de controladores ODBC] *texto de mensaje*|Administrador de controladores (odbc32. dll)|  
|Microsoft [ *Controlador ODBC: nombre*] *texto de mensaje*|ISAM del controlador (vea ISAM del controlador)|
