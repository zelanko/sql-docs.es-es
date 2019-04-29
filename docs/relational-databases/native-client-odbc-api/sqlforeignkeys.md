---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d59eb895b735771a94fa04745b492fc68eb2ea74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014517"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite las actualizaciones y eliminaciones en cascada a través del mecanismo de restricciones de clave externa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_CASCADE para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción CASCADE en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_NO_ACTION para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción NO ACTION en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY.  
  
 Cuando los valores no válidos están presentes en cualquier **SQLForeignKeys** parámetro, **SQLForeignKeys** devuelve SQL_SUCCESS en ejecución. **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLForeignKeys** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLForeignKeys** en un cursor actualizable (dinámico o conjunto de claves) devuelve SQL_SUCCESS_WITH_INFO para indicar que la que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el *FKCatalogName* y *PKCatalogName* parámetros: *Nombre_servidor_vinculado.nombre_catálogo*.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLForeignKeys](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
