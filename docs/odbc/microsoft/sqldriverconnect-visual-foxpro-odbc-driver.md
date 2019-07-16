---
title: SQLDriverConnect (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6fd8f3be1213a91195cd74a8b723629e2c5833f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053891"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Se conecta a un origen de datos existente, que puede ser un [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) o un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md). Se omiten las palabras clave de atributo ODBC UID y PWD. En la tabla siguiente se enumera las palabras clave de atributo compatibles adicionales.  
  
|Palabra clave de atributo ODBC|Valor del atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Omitido por el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|PWD|Omitido por el controlador ODBC de Visual FoxPro, pero no genera un error.|  
|Controlador|El nombre y la ubicación de Visual FoxPro ODBC Driver; implementado por el Administrador de controladores.|  
  
|Palabra clave de atributo de Visual FoxPro ODBC Driver|Valor del atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sí" o "No"|  
|Intercalar|"Equipo" o en otra secuencia de intercalación. Para obtener una lista de secuencias de intercalación admitidas, consulte [establecer intercalar](../../odbc/microsoft/set-collate-command.md).|  
|Descripción||  
|Exclusivo|"Sí" o "No"|  
|SourceDB|Una ruta de acceso completa a un directorio que contiene cero o más [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md), o el nombre de archivo y ruta absoluto para un [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" o "DBF"|  
|`Version`||  
  
 Si no se especifica el nombre del origen de datos, el Administrador de controladores pide al usuario la información (según la configuración de la *fDriverCompletion* argumento) y, a continuación, continúa. Si se necesita más información, el controlador ODBC de Visual FoxPro muestra el cuadro de diálogo.  
  
 Para obtener más información, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) en el *referencia del programador de ODBC*.
