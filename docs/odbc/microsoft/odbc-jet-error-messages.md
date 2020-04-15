---
title: Mensajes de error de ODBC Jet ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293115"
---
# <a name="odbc-jet-error-messages"></a>Mensajes de Error de Jet de ODBC
Para los errores que se producen en el origen de datos, el controlador ODBC devuelve un mensaje de error devuelto por la biblioteca de archivos ODBC. Para los errores que se producen en el controlador ODBC o el Administrador de controladores, el controlador devuelve un mensaje de error basado en el texto asociado con sqlSTATE.  
  
 Los mensajes de error tienen el siguiente formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Los prefijos entre corchetes ([ ]) identifican la ubicación del error. Cuando se produce el error en el Administrador de controladores, no se proporciona el *origen de datos.* Cuando se produce el error en el origen de datos, los prefijos [*vendor*] y [*ODBC-component*] identifican el proveedor y el nombre del componente ODBC que recibió el error del origen de datos.  
  
 En la tabla siguiente se muestran los mensajes de error devueltos por el Administrador de controladores y el controlador ISAM:  
  
|Mensaje de error|Ubicación del error|  
|-------------------|--------------------|  
|[Microsoft] [Administrador de controladores ODBC] *mensaje-texto*|Administrador de controladores (Odbc32.dll)|  
|[Microsoft] *[Nombre-controlador*ODBC ] *mensaje-texto*|Controlador ISAM (consulte ISAM del controlador)|
