---
title: Cambiar el nombre de una instancia de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ef94fc86c78e896eab03bffb318b58e4b328245
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079623"
---
# <a name="rename-an-analysis-services-instance"></a>Cambiar el nombre de una instancia de Analysis Services
  Puede cambiar el nombre de una instancia existente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizando el **cambiar el nombre de instancia** cuadro de diálogo.  
  
> [!IMPORTANT]  
>  Cuando se cambia el nombre de la instancia, la herramienta Cambiar nombre de instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecuta con privilegios elevados, actualizando el nombre de servicio de Windows, las cuentas de seguridad y las entradas de Registro asociados a esa instancia. Para garantizar que estas acciones se realizan, asegúrese de ejecutar esta herramienta como administrador del sistema local.  
  
 La herramienta Cambiar nombre de instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modifica la carpeta de programas creada para la instancia original. No modifique el nombre de la carpeta de programas para que coincida con la instancia a la que está cambiando el nombre. El cambio de una carpeta de programas puede evitar que el programa de instalación repare o desinstale la instalación.  
  
> [!NOTE]  
>  No se admite el uso de la herramienta para cambiar el nombre de instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un entorno de clúster.  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>Para cambiar el nombre de una instancia de Analysis Services  
  
1.  Iniciar el **cambiar el nombre de instancia** herramienta, **asinstancerename.exe**, desde C:\Program Files\Microsoft SQL Server\110\Tools\Binn\ManagementStudio.  
  
2.  En el cuadro de diálogo **Cambiar nombre de instancia** , seleccione en la lista **Instancia cuyo nombre se cambiará** la instancia cuyo nombre desea cambiar.  
  
3.  En el cuadro **Nuevo nombre de instancia** , escriba el nuevo nombre de la instancia.  
  
4.  Compruebe que el nombre de usuario y la contraseña son correctos y, a continuación, haga clic en **Cambiar nombre**.  
  
     La instancia de Analysis Services se detendrá y reiniciará como parte del cambio de nombre.  
  
### <a name="post-rename-checklist"></a>Lista de comprobación posterior al cambio de nombre  
  
1.  Para reanudar el acceso a las bases de datos que se ejecutan en la instancia a la que se cambia el nombre, deberá actualizar manualmente las conexiones de datos en Excel u otras aplicaciones cliente. También debe comprobar las conexiones predefinidas, como orígenes de datos compartidos de Reporting Services, archivos ODC de Exce o archivos de conexión de modelos semánticos BI, que puedan hacer referencia a la instancia cuyo nombre acaba de cambiar. Para más información, vea [Conectar a Analysis Services](connect-to-analysis-services.md).  
  
2.  Actualice los scripts de PowerShell o los scripts de AMO que utiliza habitualmente para la copia de seguridad, sincronización o procesamiento de las bases de datos.  
  
3.  Actualice las propiedades del proyecto para los proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyectos con los que trabaja en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Para las instancias de servidor en modo tabular, asegúrese de actualizar la propiedad de servidor de área de trabajo en el archivo model.bim, así como la propiedad de servidor en el proyecto.  
  
4.  Dependiendo de cómo haya especificado la cuenta de servicio, es posible que tenga que actualizar los inicios de sesión o los permisos de archivo que conceden derechos de acceso a datos en el servicio (por ejemplo, si usa la cuenta de servicio para procesar datos o para obtener acceso a objetos vinculados en otro servidor).  
  
     Será necesario actualizar un inicio de sesión o los permisos de archivo de base de datos si ha utilizado una cuenta virtual para aprovisionar el servicio. Las cuentas virtuales se basan en el nombre de instancia, por lo que si cambia el nombre de la instancia, la cuenta virtual también se actualiza al mismo tiempo. Esto significa que los inicios de sesión o permisos anteriores creados para la instancia anterior ya no son válidos.  
  
     En el ejemplo siguiente se propociona una ilustración. Supongamos que ha instalado a un servidor de modo tabular como una instancia denominada "Tabular" utilizando la cuenta virtual predeterminada, lo que resulta en la siguiente configuración:  
  
    1.  Nombre de instancia = \<servidor > \TABULAR  
  
    2.  Nombre de servicio = MSOLAP$TABULAR  
  
    3.  Cuenta virtual = NT Service\ MSOLAP$TABULAR  
  
     Ahora supongamos que cambiar el nombre de la instancia a "TAB2". Como consecuencia del cambio de nombre, la configuración podría tener ahora el siguiente aspecto:  
  
    1.  Nombre de instancia = \<servidor > \TAB2  
  
    2.  Nombre de servicio = MSOLAP$TAB2  
  
    3.  Cuenta virtual = NT Service\ MSOLAP$TAB2  
  
     Como puede ver, los permisos de base de datos y el archivo que se concedieron anteriormente a "NT Service\ MSOLAP$ TABULAR" ya no son válidos. Para garantizar que las tareas y las operaciones realizadas por el servicio se ejecutan como antes, ahora tendría debe conceder permisos de base de datos y el archivo nuevo a "NT Service\ MSOLAP$ TAB2".  
  
  
