---
title: 'Tutorial: Escribir instrucciones Transact-SQL | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 46f749029a3d2787ff30d6985770e84a08aabd86
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017478"
---
# <a name="tutorial-writing-transact-sql-statements"></a>Tutorial: Escribir instrucciones Transact-SQL
  Éste es el tutorial Escribir instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] . Este tutorial está pensado para usuarios que no tienen experiencia en escribir instrucciones SQL. Ayudará a los nuevos usuarios a empezar revisando algunas instrucciones básicas para crear tablas e insertar datos. Este tutorial usa [!INCLUDE[tsql](../includes/tsql-md.md)], la implementación de [!INCLUDE[msCoName](../includes/msconame-md.md)] del estándar SQL. Este tutorial está pensado como una breve introducción al lenguaje [!INCLUDE[tsql](../includes/tsql-md.md)] y no como una sustitución de una clase de [!INCLUDE[tsql](../includes/tsql-md.md)] . Las instrucciones de este tutorial son sencillas de forma intencionada y no pretenden representar la complejidad que se encuentra en una base de datos de producción típica.  
  
> [!NOTE]  
>  A los usuarios sin experiencia en bases de datos generalmente les resultará más fácil trabajar con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], en vez de escribir instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
## <a name="finding-more-information"></a>Buscar más información  
 Para obtener más información sobre una instrucción determinada, busque la instrucción por su nombre en los Libros en pantalla de SQL Server o use el Contenido para examinar los 1800 elementos de lenguaje enumerados alfabéticamente en [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference). Otra buena estrategia para encontrar información es buscar palabras clave relacionadas con el contenido que le interesa. Por ejemplo, si quiere conocer cómo se devuelve una parte de una fecha (como el mes), busque en el índice de **fechas [SQL Server]** y, después, seleccione **dateparts**. Esto le llevará al tema [DATEPART &#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql). Otro ejemplo sería averiguar cómo trabajar con cadenas, en cuyo caso deberá buscar **funciones de cadena**. Esto le llevará al tema [Funciones de cadena &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql).  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 Este tutorial muestra cómo crear una base de datos, crear una tabla en la base de datos, insertar datos en la tabla, actualizar, leer y eliminar datos y, a continuación, eliminar la tabla. Creará vistas y procedimientos almacenados y configurará un usuario para la base de datos y los datos.  
  
 El tutorial está compuesto por tres lecciones:  
  
 [Lección 1: Crear objetos de base de datos](lesson-1-creating-database-objects.md)  
 En esta lección, debe crear una base de datos, crear una tabla en la base de datos, insertar datos en la tabla, cambiar los datos y, a continuación, leer los datos.  
  
 [Lección 2: Configurar permisos en objetos de base de datos](lesson-2-configuring-permissions-on-database-objects.md)  
 En esta lección, debe crear un inicio de sesión y un usuario. También creará una vista y un procedimiento almacenado y, a continuación, concederá permiso al usuario para el procedimiento almacenado.  
  
 [Lección 3: Eliminar objetos de base de datos](lesson-3-1-deleting-database-objects.md)  
 En esta lección, debe quitar el acceso a datos, eliminar datos de una tabla, eliminar la tabla y, por último, eliminar la base de datos.  
  
## <a name="requirements"></a>Requisitos  
 Para completar este tutorial, no es preciso conocer el lenguaje SQL, pero deben comprenderse los conceptos básicos de base de datos, como las tablas. Durante este tutorial, creará una base de datos y un usuario de Windows. Estas tareas requieren permisos de nivel superior; por tanto, debe iniciar la sesión en el equipo como administrador.  
  
 El sistema debe tener instalado lo siguiente:  
  
-   Cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o Management Studio Express.  
  
-   Internet Explorer 6 o posterior.  
  
> [!NOTE]  
>  Cuando revise los tutoriales, le recomendamos que agregue el **siguiente** y **anterior** botones a la barra de herramientas del Visor de documentos.  
  
  
