---
title: Columnas de imagen y texto enlazado frente a sin enlazar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 306abff20146ec5004b515578f5c71b8cb574bba
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718869"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Texto delimitado frente a texto sin delimitar y columnas de imagen
  Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client está optimizado para no transmitir los datos para las columnas **Text**, **ntext**o **Image** sin enlazar en el momento en que se realiza el **SQLFetch** . Los datos **Text**, **ntext**o **Image** no se recuperan realmente del servidor hasta que la aplicación emite [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para la columna.  
  
 Se pueden escribir muchas aplicaciones para que no se muestren datos de **texto**, **ntext**o **Image** mientras un usuario simplemente se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación puede llamar a **SQLGetData** para recuperar los datos **Text**, **ntext**o **Image** . Esto evitará que se transmitan los datos **Text**, **ntext**o **Image** para cualquiera de las filas que el usuario no selecciona y, por tanto, puede evitar la transmisión de cantidades muy grandes de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
