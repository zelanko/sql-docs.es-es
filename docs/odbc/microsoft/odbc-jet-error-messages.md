---
title: Mensajes de Error de Jet ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f487fce920dd82fc36e460467733393ffdbbc36
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32901420"
---
# <a name="odbc-jet-error-messages"></a>Mensajes de Error de Jet de ODBC
Para los errores que se producen en el origen de datos, el controlador ODBC devuelve un mensaje de error devuelto por la biblioteca de archivo de ODBC. Para los errores que se producen en el controlador ODBC o el Administrador de controladores, las devoluciones de controlador un mensaje de error según el texto asociado con el valor de SQLSTATE.  
  
 Mensajes de error tienen el formato siguiente:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Los prefijos de corchetes ([]) identifican la ubicación del error. Cuando el error se produce en el Administrador de controladores, *origen de datos* no tiene. Cuando se produce el error en el origen de datos, el [*proveedor*] y [*componente ODBC*] prefijos identifican el proveedor y el nombre del componente ODBC que recibió el error del origen de datos.  
  
 La siguiente tabla muestra los mensajes de error devueltos por el Administrador de controladores y el controlador ISAM:  
  
|Mensaje de error|Ubicación del error|  
|-------------------|--------------------|  
|[Microsoft] [Administrador de controladores ODBC] *texto del mensaje*|Administrador de controladores (Odbc32.dll)|  
|[Microsoft] [ODBC *nombre del controlador*]*texto del mensaje*|Controlador ISAM (vea controlador ISAM)|
