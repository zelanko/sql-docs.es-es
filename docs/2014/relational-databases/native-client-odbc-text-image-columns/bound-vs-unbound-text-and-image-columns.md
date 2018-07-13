---
title: Texto delimitado frente a. Sin enlazar columnas Text e Image | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d77a71aae13c9601acc0ba56146e7882e6ee6e7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430634"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Texto delimitado frente a. Texto sin delimitar y columnas de imagen
  Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client está optimizado para no transmitir los datos sin delimitar **texto**, **ntext**, o **imagen** columnas en el tiempo **SQLFetch** se lleva a cabo. El **texto**, **ntext**, o **imagen** datos no se recuperan realmente desde el servidor hasta que los problemas de aplicaciones [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para el columna.  
  
 Muchas aplicaciones pueden escribirse para que ningún **texto**, **ntext**, o **imagen** se muestran los datos mientras que un usuario se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación, a continuación, puede llamar a **SQLGetData** para recuperar el **texto**, **ntext**, o **imagen** datos. Esto evitará que transmita el **texto**, **ntext**, o **imagen** datos para cualquiera de las filas que el usuario no seleccione y, por tanto, puede evitar la transmisión de muy gran tamaño cantidades de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas Text e Image](managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
