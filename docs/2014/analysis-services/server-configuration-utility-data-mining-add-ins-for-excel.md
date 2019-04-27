---
title: Utilidad de configuración del servidor (complementos de minería de datos para Excel de datos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e7a40b0cbcab787b6aa29abaa828aedcce8f5c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746807"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>Utilidad de configuración del servidor (Complementos de minería de datos para Excel)
  Al instalar los complementos de minería de datos para Excel, una utilidad de configuración del servidor también se instala y se ejecutará la primera vez que abra los complementos. En este tema se describe cómo usar la utilidad para conectarse a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y configurar una base de datos para trabajar con modelos de minería de datos.  
  

  
##  <a name="bkmk_step1"></a> Paso 1: Conectar a Analysis Services  
 Elija el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que proporciona los algoritmos de minería de datos y almacena los modelos de minería de datos.  
  
 Cuando cree una conexión para habilitar la minería de datos, debe elegir un servidor en el que pueda probar con los modelos de minería de datos. Se recomienda crear una nueva base de datos en el servidor y dedicar la nueva base de datos a la minería de datos; o bien, pida al administrador que le prepare un servidor de minería de datos. De esa forma puede crear modelos sin afectar al rendimiento de otros servicios.  
  
 Tenga en cuenta que el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que se usa para minería de datos no tiene por qué estar en el mismo servidor que los datos de origen.  
  
 **Nombre del servidor**  
 Escriba el nombre del servidor que contiene la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que usará para la minería de datos.  
  
 **Autenticación**  
 Especifique los métodos de autenticación. La autenticación de Windows es necesaria para las conexiones con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a menos que el administrador haya configurado el acceso al servidor mediante HTTPPump.  
  
##  <a name="bkmk_step2"></a> Paso 2: Permitir modelos temporales  
 Para poder usar los complementos, se debe cambiar una propiedad del servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para permitir la creación de modelos de minería de datos temporales.  
  
 Los modelos de minería de datos temporales también se denominan *modelos de sesión*. Esto se debe a que los modelos sólo se almacenan mientras la sesión actual permanece abierta. Al cerrar la conexión con el servidor, se da por finalizada la sesión y se eliminan todos los modelos que se usaron durante la misma.  
  
 El uso de modelos de minería de datos de sesión no afecta al espacio de almacenamiento del servidor, pero la sobrecarga asociada a la creación de los modelos de minería de datos puede afectar a su rendimiento.  
  
 En primer lugar, el asistente detecta la configuración en el servidor que especificó. Si el servidor ya permite modelos de minería de datos temporales, haga clic en **siguiente** para continuar. El asistente también proporciona instrucciones sobre cómo habilitar modelos de minería de datos temporales en el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificado o cómo realizar una solicitud al administrador de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_step3"></a> Paso 3: Crear base de datos para los usuarios:  
 En esta página del asistente para instalación y configuración, puede crear una base de datos nueva dedicada a la minería de datos o puede seleccionar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] existente.  
  
> [!WARNING]  
>  Minería de datos requiere una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que se ejecute en modo multidimensional. El modo tabular no admite minería de datos.  
  
 Se recomienda crear una base de datos independiente dedicada a la minería de datos. Esto le permite probar con los modelos de minería de datos sin afectar a otros objetos de la solución.  
  
 Si elige una base de datos existente en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], tenga en cuenta que se pueden sobrescribir modelos existentes si usa los complementos para crear un modelo y ya existe un modelo con dicho nombre.  
  
 **Crear nueva base de datos**  
 Seleccione esta opción para crear una base de datos nueva en el servidor seleccionado. Una base de datos de minería de datos almacenará los orígenes de datos, las estructuras de minería de datos y los modelos de minería de datos.  
  
 **Nombre de la base de datos**  
 Escriba el nombre de la nueva base de datos. Si el nombre no se está usando todavía, se creará automáticamente.  
  
 **Usar base de datos existente**  
 Seleccione esta opción para usar una base de datos existente de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Base de datos**  
 Si eligió la opción para usar una base de datos existente, debe seleccionar el nombre de la base de datos en la lista.  
  
##  <a name="bkmk_step4"></a> Paso 4: Conceder los permisos adecuados de complemento de usuarios  
 Debe asegurarse de que tanto usted como los demás usuarios que van a emplear los complementos tienen los permisos necesarios para examinar, editar, procesar o crear estructuras y modelos de minería de datos.  
  
 De forma predeterminada, para usar los complementos se requiere la autenticación integrada de Windows.  
  
 **Asigne a los usuarios agregar permisos de administración de base de datos**  
 Seleccione esta opción para conceder a los usuarios de la lista acceso administrativo a la base de datos.  
  
> [!NOTE]  
>  Estos permisos solo se aplican a la base de datos aparece en el **nombre de base de datos** cuadro.  
  
 **Nombre de la base de datos**  
 Muestra el nombre de la base de datos seleccionada.  
  
 **Especificar usuarios o grupos para agregar**  
 Seleccione los nombres de inicio de sesión que tendrán acceso a la base de datos usada para la minería de datos.  
  
 **Agregar**  
 Haga clic en esta opción para abrir un cuadro de diálogo y agregar usuarios o grupos.  
  
 **Quitar**  
 Haga clic en esta opción para quitar al usuario o al grupo seleccionado de la lista de usuarios con permisos de administración.  
  
  
