---
description: SQLDriverConnect (controlador ODBC de Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc985a5a56f54b1af8f9153bcd5129523233e2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421799"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Se conecta a un origen de datos existente, que puede ser una [base](../../odbc/microsoft/visual-foxpro-terminology.md) de datos o un directorio de [tablas disponibles](../../odbc/microsoft/visual-foxpro-terminology.md). Se omiten las palabras clave del atributo ODBC UID y PWD. En la tabla siguiente se enumeran las palabras clave de atributo compatibles adicionales.  
  
|Palabra clave de atributo ODBC|Valor del atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|El controlador ODBC de Visual FoxPro lo omite, pero no genera un error.|  
|PWD|El controlador ODBC de Visual FoxPro lo omite, pero no genera un error.|  
|Controlador|El nombre y la ubicación del controlador ODBC de Visual FoxPro; implementado por el administrador de controladores.|  
  
|Palabra clave de atributo del controlador ODBC de Visual FoxPro|Valor del atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sí" o "no"|  
|Intercalar|"Equipo" u otra secuencia de intercalación. Para obtener una lista de las secuencias de intercalación admitidas, vea [set COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descripción||  
|Exclusivo|"Sí" o "no"|  
|SourceDB|Ruta de acceso completa a un directorio que contiene cero o más [tablas libres](../../odbc/microsoft/visual-foxpro-terminology.md), o la ruta de acceso absoluta y el nombre de archivo de una [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" o "DBF"|  
|Versión||  
  
 Si no se especifica el nombre del origen de datos, el administrador de controladores solicita al usuario la información (dependiendo de la configuración del argumento *fDriverCompletion* ) y, a continuación, continúa. Si se requiere más información, el controlador ODBC de Visual FoxPro muestra el cuadro de diálogo de solicitud.  
  
 Para obtener más información, vea [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) en la *Referencia del programador de ODBC*.
