---
title: Cambio de la plataforma de destino y publicación de un proyecto de base de datos | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.publish.dialog
- sql.data.tools.publishdacproject
ms.assetid: 6012e120-5f72-4f4f-ae6e-f9a57ae1dea7
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 91bb424e4bb9e3da25a53e5080db6fbe2e2a6e53
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094781"
---
# <a name="how-to-change-target-platform-and-publish-a-database-project"></a>Cómo: Cambiar la plataforma de destino y publicar un proyecto de base de datos
Puede cambiar la versión de SQL Server de destino para su proyecto de base de datos SQL Server Data Tools (SSDT) por cualquier instancia compatible de SQL Server (SQL Server 2005, 2008, 2008 R2, Microsoft SQL Server 2012 o SQL Azure). De esta forma, puede centralizar el desarrollo de base de datos en un proyecto y publicarlo en varios tipos de instancias de SQL Server si es necesario.  
  
SSDT también simplifica esta tarea, ya que reconoce la plataforma de destino y detecta automáticamente cualquier error en el código (por ejemplo, cuando se usan características no admitidas para un proyecto que se va a publicar en SQL Azure).  
  
> [!WARNING]  
> Los procedimientos siguientes usan entidades creadas en procedimientos anteriores de las secciones [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md) y [Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-change-a-projects-target-platform"></a>Para cambiar la plataforma de destino de un proyecto  
  
1.  Haga clic con el botón derecho en el proyecto en el **Explorador de soluciones** y seleccione **Propiedades**. Haga clic en la pestaña **Configuración del proyecto** de la izquierda para tener acceso a la página de propiedades **Configuración del proyecto** .  
  
2.  La lista desplegable **Plataforma de destino** de esta página contiene todas las plataformas de SQL Server admitidas en las que se puede publicar un proyecto de base de datos. Para este procedimiento, seleccione **SQL Azure**.  
  
### <a name="to-use-platform-validation-when-editing-scripts"></a>Para usar la validación de la plataforma al editar scripts  
  
1.  Haga clic con el botón derecho en la tabla **Products** en el Explorador de soluciones y seleccione **Ver código** para abrirlo en el Editor de Transact\-SQL.  
  
2.  Anexe `ON [PRIMARY]` al final de la instrucción `CREATE TABLE` .  
  
3.  Observe que aparece el siguiente error en el panel **Lista de errores**: SQL70015: 'Referencia de grupo de archivos y esquema de partición' no se admite en SQL Azure.  
  
    SSDT valida automáticamente el script según la plataforma de destino. En este caso, como el grupo de archivos no se admite en SQL Azure, SSDT devuelve un error. Para obtener una lista de instrucciones Transact\-SQL no admitidas en SQL Azure, consulte [Instrucciones Transact-SQL admitidas parcialmente (Microsoft Azure SQL Database)](http://msdn.microsoft.com/en-us/library/ee336267.aspx).  
  
4.  Quite la cláusula `ON` . Observe que el error desaparece inmediatamente de la **Lista de errores**.  
  
### <a name="to-publish-a-database-project"></a>Para publicar un proyecto de base de datos  
  
1.  Si tiene acceso a una instancia de SQL Azure, puede ir al siguiente paso. De lo contrario, haga clic con el botón derecho en el proyecto **TradeDev** en el **Explorador de soluciones** y seleccione **Propiedades** para tener acceso a la página de propiedades **Configuración del proyecto**. Use la lista desplegable **Plataforma de destino** para seleccionar la plataforma de SQL Server en la que desea publicar el proyecto.  
  
2.  Haga clic con el botón derecho en el proyecto **TradeDev** en el **Explorador de soluciones** y seleccione **Publicar**. SSDT empezará a compilar el proyecto. Si no hay ningún error de compilación, aparecerá el cuadro de diálogo **Publicar base de datos** .  
  
3.  En el cuadro de diálogo **Publicar base de datos** , haga clic en **Editar** para editar la conexión de la base de datos de destino.  
  
4.  En el cuadro de diálogo **Propiedades de la conexión**, escriba el nombre de la instancia de SQL Server y las credenciales de autenticación. En **Conectar con una base de datos**, escriba **NewTrade**. Esto intentará publicar el proyecto de base de datos en una base de datos nueva. También puede elegir una base de datos existente en la que realizar la publicación. Por ejemplo, si elige la base de datos existente **TradeDev**, todos los cambios que haya realizado en los objetos (como scripts) en el proyecto **TradeDev** sin conexión se propagarán a la base de datos **TradeDev** activa.  
  
    Si tiene permiso para realizar cambios en la base de datos en la que desea publicar, haga clic en el botón **Publicar** . Sin embargo, si no tiene acceso de escritura a una base de datos de producción, puede hacer clic en el botón **Generar script** para generar un script de publicación de Transact\-SQL, que se puede entregar a un DBA. Entonces, el DBA puede ejecutar el script para actualizar el servidor de producción de forma que su esquema esté sincronizado con el proyecto de base de datos.  
  
5.  La ventana **Operaciones de herramientas de datos**  mostrará el progreso de sus operaciones de publicación y le notificará de posibles errores. En esta nueva ventana también puede elegir entre ver la vista previa de implementación, el script generado o todos los resultados de publicación si lo desea.  
  
6.  También puede guardar la configuración de publicación en un perfil, de manera que pueda reutilizar la misma configuración para futuras operaciones de publicación. Para ello, haga clic en el botón **Guardar perfil como** del cuadro de diálogo **Publicar base de datos** . En el futuro, puede hacer clic en el botón **Cargar perfil** cuando desee volver a cargar configuraciones existentes.  
  
7.  Observe los mensajes de la ventana **Operaciones de Data Tools** . Hacer clic en el vínculo “Vista previa” a la derecha de **Creando vista previa de publicación…** Se abrirá el informe de vista previa de implementación. Si la plataforma de destino del proyecto no es idéntica al servidor de bases de datos en la que se publica el proyecto, SSDT generará una advertencia en este informe.  Por ejemplo, si la plataforma de destino del proyecto es Microsoft SQL Server 2012 y está intentando publicar el proyecto en una instancia de servidor de SQL Server 2008 R2, verá la advertencia siguiente en la ventana **Salida**:  
  
**Un proyecto que especifique Microsoft SQL Server 2012 como plataforma de destino puede experimentar problemas de compatibilidad con SQL Server 2008**. Si dicho proyecto contiene entidades (por ejemplo, un objeto Sequence) que se introducen en Microsoft SQL Server 2012, se producirá un error en la operación de publicación.  
  
    The deployment will fail if object predicates use **CONTAINS** or **FREETEXT** over a newly created full-text index and transactional scripts are used. If the option to include transactional scripts is enabled during deployment, then procedures and views are defined inside a transaction while a full-text index is defined outside of a transaction at the end of the deploy script. Because of this ordering in the script, procedures or views using CONTAINS or FREETEXT will not be resolved against the full-text index, resulting in a deployment error.  
  
