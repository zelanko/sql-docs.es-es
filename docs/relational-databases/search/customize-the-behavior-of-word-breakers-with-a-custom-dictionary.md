---
title: "Personalización del comportamiento de separadores de palabras con un diccionario personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9325fc9817b8c0f57ebeb9c6a0e9ae8f29b899cc
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizar el comportamiento de separadores de palabras con un diccionario personalizado
  Puede personalizar el comportamiento del separador de palabras para un idioma determinado creando un archivo de diccionario personalizado específico del idioma. Por ejemplo, puede evitar que el separador de palabras separe algunos términos o patrones.  
  
 Para obtener más información, vea el artículo siguiente de SharePoint:  
  
 [Cree un diccionario personalizado (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque los archivos de diccionario personalizado en la siguiente carpeta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Después de crear o cambiar los archivos de diccionario personalizado, reinicie el Selector de demonio de filtro de texto completo de SQL con el comando siguiente:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
