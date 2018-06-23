---
title: Frente a enlazado. Sin enlazar columnas Text e Image | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5129c6b865723721bbb6f176893c950cdf905fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106735"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Frente a enlazado. Columnas sin enlazar Text e Image
  Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client está optimizado para no transmitir los datos sin delimitar **texto**, **ntext**, o **imagen** columnas en la tiempo **SQLFetch** se lleva a cabo. El **texto**, **ntext**, o **imagen** datos no se recuperan realmente desde el servidor hasta que los problemas de aplicaciones [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para el columna.  
  
 Muchas aplicaciones se pueden escribir para que no **texto**, **ntext**, o **imagen** se muestran los datos mientras un usuario se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación, a continuación, puede llamar a **SQLGetData** para recuperar la **texto**, **ntext**, o **imagen** datos. Esto evitará que transmitir la **texto**, **ntext**, o **imagen** datos para cualquiera de las filas, el usuario no seleccione y, por tanto, evitar la transmisión de grandes cantidades de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas Text e Image](managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  