---
title: catalog.get_project (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ff4114aef15313606ac6cf03c7f7d56d407dcf3
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295418"
---
# <a name="catalogget_project-ssisdb-database"></a>catalog.get_project (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Recupera el flujo binario de un proyecto que se ha implementado en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el proyecto. *folder_name* es **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto. *project_name* es **nvarchar(128)** .  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 El flujo binario del proyecto se devuelve como **varbinary(MAX)** . No se devuelve ningún resultado si no se encuentra la carpeta o el proyecto.  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen algunas condiciones que pueden hacer que el procedimiento almacenado get_project produzca un error:  
  
-   El proyecto no existe  
  
-   La carpeta no existe  
  
-   El usuario no tiene los permisos adecuados.  
  
  
