---
description: Personalización del comportamiento de los separadores de palabras con un diccionario personalizado (Búsqueda de SQL Server)
title: Personalización del comportamiento de los separadores de palabras con un diccionario personalizado
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 46fb0f6fa4e8607296ead7a2f5e77ac97e75f9d5
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866991"
---
# <a name="customize-behavior-of-word-breakers-with-a-custom-dictionary-sql-server-search"></a>Personalización del comportamiento de los separadores de palabras con un diccionario personalizado (Búsqueda de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Puede personalizar el comportamiento del separador de palabras para un idioma determinado creando un archivo de diccionario personalizado específico del idioma. Por ejemplo, puede evitar que el separador de palabras separe algunos términos o patrones.  
  
 Para obtener más información, vea el artículo siguiente de SharePoint:  
  
 [Cree un diccionario personalizado (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/cc263242(v=office.14))  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque los archivos de diccionario personalizado en la siguiente carpeta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Después de crear o cambiar los archivos de diccionario personalizado, reinicie el Selector de demonio de filtro de texto completo de SQL con el comando siguiente:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
