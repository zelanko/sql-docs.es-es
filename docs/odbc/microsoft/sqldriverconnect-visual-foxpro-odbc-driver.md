---
title: SQLDriverConnect (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307096"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 1  
  
 Se conecta a un origen de datos existente, que puede ser una base de [datos](../../odbc/microsoft/visual-foxpro-terminology.md) o un directorio de [tablas libres.](../../odbc/microsoft/visual-foxpro-terminology.md) Se omiten las palabras clave de atributo ODBC UID y PWD. En la tabla siguiente se enumeran las palabras clave de atributo admitidas adicionales.  
  
|Palabra clave de atributo ODBC|Valor del atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorado por el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|PWD|Ignorado por el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|Controlador|El nombre y la ubicación del controlador ODBC de Visual FoxPro; implementado por el Administrador de controladores.|  
  
|Palabra clave de atributo controlador ODBC de Visual FoxPro|Valor del atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sí" o "No"|  
|Intercalar|"Máquina" u otra secuencia de intercalación. Para obtener una lista de las secuencias de intercalación admitidas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descripción||  
|Exclusivo|"Sí" o "No"|  
|SourceDB|Una ruta de acceso completa a un directorio que contiene cero o más [tablas libres,](../../odbc/microsoft/visual-foxpro-terminology.md)o la ruta de acceso absoluta y el nombre de archivo de una base de [datos.](../../odbc/microsoft/visual-foxpro-terminology.md)|  
|SourceType|"DBC" o "DBF"|  
|Versión||  
  
 Si no se especifica el nombre del origen de datos, el Administrador de controladores solicita al usuario la información (dependiendo de la configuración del argumento *fDriverCompletion)* y, a continuación, continúa. Si se requiere más información, el controlador ODBC de Visual FoxPro muestra el cuadro de diálogo de solicitud.  
  
 Para obtener más información, vea [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) en la *referencia del programador ODBC*.
