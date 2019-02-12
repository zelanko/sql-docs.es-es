---
title: Seguridad de DQS | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 266c491b4e47ff525d05e80a6044705257c0ffb6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036166"
---
# <a name="dqs-security"></a>Seguridad de DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La infraestructura de seguridad de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) está basada en la infraestructura de seguridad de SQL Server. Un administrador de bases de datos concede al usuario un conjunto de permisos mediante la asociación de dicho usuario a un rol de DQS. De este modo, determina los recursos de DQS a los que el usuario tiene acceso y las actividades funcionales que este puede realizar.  
  
## <a name="dqs-roles"></a>Roles de DQS  
 Existen cuatro roles para DQS. Uno es el administrador de bases de datos (DBA), que se ocupa principalmente de la instalación del producto, el mantenimiento de las bases de datos y la administración de los usuarios. Este rol se usa principalmente en SQL Server Management Studio en lugar de en la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Su rol de servidor es sysadmin.  
  
 Los otros tres roles son trabajadores de la información, administradores de datos que utilizan el producto trabajando directamente en la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Estos roles son los siguientes:  
  
-   El **Administrador de DQS** (rol dqs_administrator) puede realizar cualquier tarea dentro del ámbito del producto. El administrador puede modificar y ejecutar un proyecto, crear y modificar una base de conocimiento, terminar una actividad, detener un proceso dentro de una actividad y cambiar la configuración de Reference Data Services. El Administrador de DQS no puede, no obstante, instalar el servidor ni agregar nuevos usuarios. Es el administrador de bases de datos quien debe hacerlo.  
  
-   El **Editor de KB de DQS** (rol dqs_kb_editor) puede realizar todas las actividades de DQS, a excepción de la administración. El Editor de KB puede modificar y ejecutar un proyecto, y crear y modificar una base de conocimiento. Puede ver los datos de supervisión de las actividades, pero no puede terminar ni detener una actividad ni realizar labores administrativas.  
  
-   El **Operador de KB de DQS** (rol dqs_kb_operator) puede modificar y ejecutar un proyecto. No puede realizar ningún tipo de tarea relacionada con la administración del conocimiento, ni puede crear ni cambiar una base de conocimiento. Puede ver los datos de supervisión de las actividades, pero no puede terminar una actividad ni realizar labores administrativas.  
  
## <a name="user-management"></a>Administración de usuarios  
 El administrador de bases de datos (DBA) crea usuarios de DQS y los asocia a roles de DQS en SQL Server Management Studio. Para administrar los permisos, el DBA agrega inicios de sesión de SQL como usuarios de la base de datos DQS_MAIN y asocia cada usuario a uno de los roles de DQS. A cada rol se le conceden permisos de acceso a un conjunto de procedimientos almacenados de la base de datos DQS_MAIN. Los tres roles de DQS no están disponibles para las bases de datos DQS_PROJECTS y DQS_STAGING_DATA.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo crear un usuario y cómo concederle roles de DQS mediante SQL Server Management Studio.|[Administrar usuarios de DQS en SSMS](https://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  
