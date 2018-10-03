---
title: Los mensajes de Error de Jet de ODBC | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ec549f256caeab598f6e49632b2a50cfa5841710
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620283"
---
# <a name="odbc-jet-error-messages"></a>Mensajes de Error de Jet de ODBC
Para los errores que se producen en el origen de datos, el controlador ODBC devuelve un mensaje de error devuelto por la biblioteca de archivos de ODBC. Errores que se producen en el controlador ODBC o el Administrador de controladores, las devoluciones de controlador un mensaje de error según el texto asociado con el valor de SQLSTATE.  
  
 Los mensajes de error tienen el formato siguiente:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Los prefijos de corchetes ([]) identifican la ubicación del error. El error se produce en el Administrador de controladores, *origen de datos* no tiene. Cuando se produce el error en el origen de datos, el [*proveedor*] y [*componentes ODBC*] prefijos identifican el proveedor y el nombre del componente ODBC que recibió el error del origen de datos.  
  
 La siguiente tabla muestra los mensajes de error devueltos por el Administrador de controladores y el controlador ISAM:  
  
|Mensaje de error|Ubicación del error|  
|-------------------|--------------------|  
|[Microsoft] [Administrador de controladores ODBC] *texto del mensaje*|Administrador de controladores (Odbc32.dll)|  
|[Microsoft] [ODBC *nombre del controlador*]*texto del mensaje*|El controlador ISAM (consulte el controlador ISAM)|
