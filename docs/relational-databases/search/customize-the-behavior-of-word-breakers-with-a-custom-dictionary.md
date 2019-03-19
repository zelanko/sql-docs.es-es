---
title: Personalización del comportamiento de separadores de palabras con un diccionario personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 957b9e6834e4f590a1ef71a515d287a88fe6cc93
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973774"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizar el comportamiento de separadores de palabras con un diccionario personalizado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede personalizar el comportamiento del separador de palabras para un idioma determinado creando un archivo de diccionario personalizado específico del idioma. Por ejemplo, puede evitar que el separador de palabras separe algunos términos o patrones.  
  
 Para obtener más información, vea el artículo siguiente de SharePoint:  
  
 [Cree un diccionario personalizado (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque los archivos de diccionario personalizado en la siguiente carpeta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Después de crear o cambiar los archivos de diccionario personalizado, reinicie el Selector de demonio de filtro de texto completo de SQL con el comando siguiente:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
