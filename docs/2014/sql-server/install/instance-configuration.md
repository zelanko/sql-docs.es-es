---
title: Configuración de instancia | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66329d4c25a23a6b3dbc3570723bab8aecfa3d4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68190964"
---
# <a name="instance-configuration"></a>Configuración de instancia
  Use la página **Configuración de instancia** del Asistente para instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de especificar si quiere crear una instancia predeterminada o una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si aún no hay instalada ninguna instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se creará una predeterminada, a menos que especifique una instancia con nombre.  
  
 Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consta de un conjunto de servicios distinto con una configuración específica para intercalaciones y otras opciones. La estructura de directorios, la estructura del Registro y los nombres de los servicios reflejan todos el nombre de instancia y un identificador de instancia específico que se crearon durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La instancia puede ser una instancia predeterminada o una instancia con nombre. El nombre de instancia predeterminado es MSSQLSERVER. Para realizar una conexión, no es necesario que un cliente especifique el nombre de la instancia. La instancia con nombre queda determinada por el usuario durante la instalación. Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como una instancia con nombre sin instalar primero la instancia predeterminada. Al mismo tiempo, solo una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de la versión, puede ser la instancia predeterminada.  
  
 **OnAlert!** Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, puede especificar el nombre de instancia cuando complete una instancia preparada en la página **Configuración de instancia**. Puede optar por configurar la instancia preparada que está completando como una instancia predeterminada si no existe una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo.  
  
## <a name="multiple-instances"></a>Instancias múltiples  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un solo servidor o procesador, pero solo una puede ser la predeterminada. Todas las demás deben ser instancias con nombre. Un equipo puede ejecutar varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultáneamente y cada instancia se ejecuta independientemente de las otras instancias.  
  
 Para obtener más información, vea [Especificaciones de capacidad máxima para SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
## <a name="options"></a>Opciones  
 Solo instancias de clústeres de conmutación por error: especifique el nombre de red en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este nombre identifica la instancia en clúster de conmutación por error en la red.  
  
 Instancia predeterminada o con nombre: tenga presente la información siguiente a la hora de decidir entre instalar una instancia predeterminada o una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si piensa instalar una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor de base de datos, debe ser una instancia predeterminada.  
  
-   Use una instancia con nombre para aquellas situaciones en las que piensa tener varias instancias en el mismo equipo. Un servidor solo puede alojar una instancia predeterminada.  
  
-   Cualquier aplicación que instale [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] debe instalarla como instancia con nombre. Con ello se reducen los conflictos en situaciones en las que se instalan varias aplicaciones en el mismo equipo.  
  
 **Instancia predeterminada**  
 Seleccione esta opción para instalar una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un equipo solo puede hospedar una instancia predeterminada; todas las demás instancias deben ser instancias con nombre. No obstante, si tiene instalada una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podrá agregar una instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al mismo equipo.  
  
 **Instancia con nombre**  
 Seleccione esta opción para crear una instancia con nombre nueva. Cuando asigne un nombre a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenga en cuenta lo siguiente:  
  
-   En los nombres de instancia no se distinguen mayúsculas y minúsculas.  
  
-   Los nombres no pueden comenzar ni terminar por un guión bajo (_).  
  
-   Los nombres de instancia no pueden contener el término "Default" ni otras palabras clave reservadas. Si se utiliza una palabra clave reservada en un nombre de instancia, se producirá un error en el programa de instalación. Para obtener más información, vea [palabras clave reservadas &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql).  
  
-   Si especifica MSSQLServer como nombre de instancia, se creará una instancia predeterminada.  
  
-   Una instalación de [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] siempre se instala como una instancia con nombre de 'PowerPivot'. No puede especificar un nombre de instancia diferente para este rol de característica.  
  
-   Los nombres de instancias están limitados a 16 caracteres.  
  
-   El primer carácter del nombre de la instancia debe ser una letra. Las letras aceptables son las que define el estándar Unicode 2.0. Se incluyen los caracteres latinos, a-z, A-Z y los caracteres alfabéticos de otros idiomas.  
  
-   Los siguientes caracteres pueden ser letras definidas por el estándar Unicode 2.0, números decimales del alfabeto Latín básico y de otros alfabetos nacionales, el signo de dólar ($) o un carácter de subrayado (_).  
  
-   En los nombres de instancia no se permiten espacios insertados ni otros caracteres especiales. Tampoco se permiten la barra diagonal inversa (\\), la coma (,), los dos puntos (:), el punto y coma (;), la comilla simple ('), el símbolo Y comercial (&), el guion (-) ni la arroba (@).  
  
-   **En los nombres de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia solo se pueden usar caracteres que sean válidos en la página de códigos actual de Windows. Si se utiliza un carácter Unicode no admitido, se producirá un error en el programa de instalación.**  
  
 **Instancias y características detectadas**  
 Vea una lista de las instancias y los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados en el equipo en el que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **ID** . de instancia: de forma predeterminada, el nombre de instancia se usa como identificador de instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para usar un identificador de instancia no predeterminado, especifíquelo en el campo **ID** . de instancia.  
  
> [!IMPORTANT]  
>  Con SysPrep de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el identificador de instancia que se muestra en esta página es el identificador de instancia especificado durante el paso de preparación de la imagen en el proceso SysPrep de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No podrá especificar un identificador de instancia diferente durante el paso para completar la imagen.  
  
> [!NOTE]  
>  No se admiten identificadores de instancia que comiencen por un guión bajo (_) o que contengan el signo de almohadilla (#) o el signo de dólar ($).  
  
 Para obtener más información acerca de los directorios, las ubicaciones de archivos y los nombres de IDENTIFICADOres de instancia, vea [ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Todos los componentes de una instancia determinada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se administran como una unidad. Todos los Service Pack y actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicarán a cada componente de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que comparten el mismo nombre de instancia deben cumplir los siguientes criterios:  
  
-   **Misma versión**  
  
-   **Misma edición**  
  
-   **Misma configuración de idioma**  
  
-   **Mismo estado en clúster**  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no detecta los clústeres.  
  
-   **Mismo sistema operativo**  
  
  
