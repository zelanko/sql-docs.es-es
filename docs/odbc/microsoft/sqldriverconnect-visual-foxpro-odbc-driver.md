---
title: SQLDriverConnect (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 363a727cd209f7ed3a5994f353f1e21922fe00ca
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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

