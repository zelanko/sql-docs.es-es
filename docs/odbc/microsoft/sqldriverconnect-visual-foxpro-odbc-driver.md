---
title: SQLDriverConnect (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1aedce0d1e2888a4aada3a92cf0eb5973d489a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Se conecta a un origen de datos existente, que puede ser un [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) o un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md). Se omiten las palabras clave de atributo ODBC UID y PWD. En la tabla siguiente se enumera las palabras clave de atributo compatibles adicionales.  
  
|Palabra clave de atributo ODBC|Valor del atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Omite el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|PWD|Omite el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|Controlador|El nombre y la ubicación de Visual FoxPro ODBC Driver; implementado por el Administrador de controladores.|  
  
|Palabra clave de atributo de controlador ODBC de FoxPro Visual|Valor del atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sí" o "No"|  
|Intercalar|"Equipo" o en otra secuencia de intercalación. Para obtener una lista de secuencias de intercalación admitidas, consulte [establecer COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Description||  
|Exclusivo|"Sí" o "No"|  
|SourceDB|Una ruta de acceso completa a un directorio que contiene cero o más [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md), o el nombre de archivo y ruta absoluto para una [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|Tipo de origen|"DBC" o "DBF"|  
|Versión||  
  
 Si no se especifica el nombre de origen de datos, el Administrador de controladores pide al usuario la información (según la configuración de la *fDriverCompletion* argumento) y, a continuación, continúa. Si se necesita más información, el controlador ODBC de Visual FoxPro muestra el cuadro de diálogo.  
  
 Para obtener más información, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) en el *referencia del programador de ODBC*.
