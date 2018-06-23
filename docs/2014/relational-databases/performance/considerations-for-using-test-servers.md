---
title: Consideraciones acerca del uso de servidores de prueba | Microsoft Docs
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
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 810ad8d5d3d977d49469e441efff0b5189c0e4f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105833"
---
# <a name="considerations-for-using-test-servers"></a>Consideraciones acerca del uso de servidores de prueba
  El uso de un servidor de prueba para optimizar una base de datos en un servidor de producción es una ventaja importante del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Mediante esta característica se puede descargar la sobrecarga de optimización en un servidor de prueba sin copiar los datos reales del servidor de producción a ese servidor de prueba.  
  
> [!NOTE]  
>  La característica de optimización del servidor de prueba no se admite en la interfaz gráfica de usuario (GUI) del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Para utilizar correctamente esta característica, revise las consideraciones enumeradas en las siguientes secciones:  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>Configurar el entorno del servidor de prueba/servidor de producción  
  
-   El usuario que desea utilizar un servidor de prueba para optimizar una base de datos de un servidor de producción debe existir en ambos servidores; de lo contrario, este escenario no funcionará.  
  
-   El procedimiento almacenado extendido, **xp_msver**, debe estar habilitado para usar el escenario del servidor de prueba/servidor de producción. [!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza este procedimiento almacenado extendido para capturar el número de procesadores y la memoria disponible del servidor de producción para utilizarlos durante la optimización del servidor de prueba. Si **xp_msver** no está habilitado, el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] adopta las características de hardware del equipo donde se está ejecutando el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Si no están disponibles las características de hardware del equipo donde se está ejecutando el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , se presupone el uso de un procesador y 1024 megabytes (MB) de memoria. Este procedimiento almacenado extendido se activa de manera predeterminada al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [Surface Area Configuration](../security/surface-area-configuration.md) y [xp_msver &#40;Transact-SQL&#41;] (~ / relational-databases/system-stored-procedures/xp-msver-transact-sql.md.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] espera que las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sean las mismas en el servidor de prueba y el servidor de producción. Si hay ediciones diferentes, tiene prioridad la edición del servidor de prueba. Por ejemplo, si el servidor de prueba está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard, el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no incluirá vistas indizadas, particionamientos ni operaciones en línea en sus recomendaciones, aunque el servidor de producción esté ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise.  
  
## <a name="about-test-serverproduction-server-behavior"></a>Comportamiento del servidor de prueba/servidor de producción  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] tiene en cuenta las diferencias de hardware entre el servidor de producción y el de prueba a la hora de crear recomendaciones. La recomendación es la misma que si se hubiera realizado la optimización solo en el servidor de producción.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede imponer cierta carga al servidor de producción a la hora de recopilar metadatos y crear las estadísticas necesarias para la optimización.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] no copia datos reales del servidor de producción al servidor de prueba. Solo copia los metadatos de las bases de datos y las estadísticas necesarias.  
  
-   Toda la información de la sesión se almacena en **msdb** en el servidor de producción. Esto permite explotar cualquier servidor de prueba disponible para la optimización, y la información sobre todas las sesiones está disponible en un mismo lugar (el servidor de producción).  
  
## <a name="issues-related-to-the-shell-database"></a>Problemas relacionados con la base de datos de shell  
  
-   Tras la optimización, el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe quitar todos los metadatos que creó en el servidor de prueba durante el proceso de optimización. Esto incluye la base de datos de shell. Si está realizando una serie de sesiones de optimización con los mismos servidores de producción y de prueba, es posible que desee mantener esta base de datos de shell para ahorrar tiempo. En el archivo de entrada XML, especifique el subelemento **RetainShellDB** con los demás subelementos del elemento primario **TuningOptions** . El uso de estas opciones hace que el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] mantenga la base de datos de shell. Para obtener más información, vea [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](database-engine-tuning-advisor.md).  
  
-   Después de una sesión de optimización correcta en un servidor de producción o de prueba, pueden quedar bases de datos de shell en el servidor de prueba, aunque no se haya especificado la opción **RetainShellDB**. Estas bases de datos de shell no deseadas pueden interferir con las sesiones de optimización posteriores y se deben quitar antes de ejecutar otra sesión de optimización del servidor de prueba o de producción. Además, si una sesión de optimización se cierra de forma inesperada, las bases de datos de shell en el servidor de prueba y los objetos que hay en esas bases de datos se pueden quedar en el servidor de prueba. También debe eliminar estas bases de datos y objetos antes de iniciar una nueva sesión de optimización del servidor de prueba o de producción.  
  
## <a name="issues-related-to-the-tuning-process"></a>Problemas relacionados con el proceso de optimización  
  
-   El usuario debe comprobar si el registro de optimización contiene errores de optimización derivados de las diferencias entre los servidores de producción y de prueba, y errores derivados de copiar metadatos del servidor de producción en el de prueba. Por ejemplo, es posible que no exista ningún inicio de sesión de usuario en el servidor de prueba. Si no existe ningún inicio de sesión de usuario en el servidor de prueba, es posible que los eventos de la carga de trabajo emitidos por ese inicio de sesión de usuario no puedan optimizarse. Utilice la GUI del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para ver el registro de optimización. Para obtener más información, vea [Ver y trabajar con la salida del Asistente para la optimización de motor de base de datos](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
-   Si el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no puede optimizar muchos eventos porque faltan objetos en la base de datos de shell que crea el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el servidor de prueba, el usuario debe comprobar el registro de optimización. Los eventos que no se pueden optimizar aparecen en el registro. Para optimizar correctamente la base de datos en el servidor de prueba, el usuario debe crear los objetos que faltan en la base de datos de shell y, a continuación, iniciar una nueva sesión de optimización.  
  
-   Si ya existe una base de datos con el mismo nombre en el servidor de prueba, el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no copia los metadatos, sino que sigue optimizando y recopila las estadísticas según sea necesario. Esto resulta útil si el usuario ya ha creado una base de datos en el servidor de prueba y ha copiado los metadatos apropiados antes de invocar al Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Si la opción DATE_CORRELATION_OPTIMIZATION está activada para una base de datos en el servidor de producción, no se genera un script completo de los metadatos y los datos asociados a esta opción durante la optimización del servidor de prueba. Cuando se lleva a cabo la optimización para un escenario de servidor de prueba/servidor de producción, es posible que surjan los problemas siguientes:  
  
    -   Los usuarios pueden tener distintos planes de consulta en los servidores para las consultas que utilizan la opción DATE_CORRELATION_OPTIMIZATION.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] El Asistente para la optimización puede sugerir que se quiten las vistas indexadas que fuerzan la opción DATE_CORRELATION_OPTIMIZATION en el script de recomendación.  
  
     Por lo tanto, es posible que desee omitir las recomendaciones que haga el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] sobre las vistas indizadas que mantienen las estadísticas de correlación porque el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] conoce sus costos, pero no sus ventajas. [!INCLUDE[ssDE](../../includes/ssde-md.md)] Es posible que el Asistente para la optimización no recomiende la selección de ciertos índices, como los índices agrupados en las columnas **datetime** , lo que puede ser beneficioso cuando la opción DATE_CORRELATION_OPTIMIZATION está habilitada.  
  
     Para saber si una vista se basa en las estadísticas de correlación, seleccione la columna **is_date_correlation_view** de la vista de catálogo [sys.views](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) .  
  
  
