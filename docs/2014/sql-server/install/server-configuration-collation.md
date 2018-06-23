---
title: Configurar servidor - intercalación | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ee24c8f9234069526780db72457e178d50d5c824
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203804"
---
# <a name="server-configuration---collation"></a>Configurar servidor - Intercalación
  En la página Configuración del servidor - Intercalación del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede modificar los valores de intercalación que [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizan para la ordenación. Seleccione la opción que coincida con los valores de intercalación de distintas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o de otro equipo.  
  
## <a name="options"></a>Opciones  
 Personalizar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona dos grupos de intercalaciones: las intercalaciones de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intercalaciones. Puede especificar unos valores de intercalación independientes para el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o puede especificar la misma intercalación para ambos.  
  
 De forma predeterminada, se selecciona una intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las configuraciones regionales en idioma inglés. El valor de configuración regional del sistema de Windows del equipo determina la intercalación predeterminada de las versiones localizadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La configuración predeterminada solo se debería cambiar si la configuración de intercalación de esta instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe coincidir con la que usa otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o con la configuración regional de Windows de otro equipo.  
  
 **Nota** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo usa las intercalaciones de Windows. Si piensa instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seleccione una intercalación de Windows durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para asegurarse de que los resultados son coherentes entre [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://go.microsoft.com/fwlink/?LinkId=190977).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Para obtener más información acerca de una tabla de configuraciones regionales del sistema de Windows y las intercalaciones predeterminadas correspondientes utilizadas por el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Configuración de intercalación en el programa de instalación](http://go.microsoft.com/fwlink/?LinkId=190977).  
  
 Si es posible, utilice una sola intercalación para su organización. De esta manera no tiene que especificar explícitamente la intercalación para cada base de datos, columna, expresión o identificador. Si tiene que trabajar con varias intercalaciones y configuraciones de páginas de códigos distintas, codifique sus consultas para que tengan en cuenta las reglas de prioridad de intercalación. Para obtener más información, vea el tema de los Libros en pantalla correspondiente a [Prioridad de intercalación &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql).  
  
 Al seleccionar una intercalación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere las recomendaciones siguientes:  
  
-   Seleccione una intercalación BINARY2 si la ordenación basada en el punto de código binario es aceptable.  
  
-   Seleccione una intercalación de Windows para realizar una comparación coherente a través de los tipos de datos.  
  
-   Use la nueva intercalación de nivel 100 para permitir una mejor ordenación lingüística. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Si piensa migrar una base de datos a una instancia actualizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione la intercalación que coincida con la intercalación existente de la base de datos.  
  
  
