---
title: "Cuadro de diálogo Crear nueva directiva o Abrir directiva, página General | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 17c975de731604cb3bec9586735b344f532a50ab
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>Cuadro de diálogo Crear nueva directiva o Abrir directiva, página General
  Utilice este cuadro de diálogo para crear una directiva nueva de administración basada en directivas o modificar una directiva existente. Utilice las áreas **Para destinos** y **Restricción de servidor** como filtro para limitar las directivas a un subconjunto de todos los destinos posibles. Las condiciones que se usan como filtros de destino se deben definir en una faceta física y no deben contener funciones ni el operador LIKE. Cuando el sistema calcula el conjunto de objetos para una directiva, los objetos del sistema se excluyen de forma predeterminada.  Por ejemplo, si el conjunto de objetos de la directiva hace referencia a todas las tablas, la directiva no se aplicará a las tablas del sistema. Si los usuarios desean evaluar una directiva con los objetos del sistema, pueden agregar explícitamente objetos del sistema al conjunto de objetos. Sin embargo, aunque se admiten todas las directivas para el modo de evaluación **Comprobar en la programación** , por razones de rendimiento, no todas las directivas con conjuntos de objetos arbitrarios se admiten para el modo de evaluación **Comprobar en los cambios** . Para obtener más información, vea [http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Si la directiva es nueva, escriba un nombre para ella. Si la directiva ya existe, se muestra el nombre.  
  
 **Habilitado**  
 Active la casilla **Habilitada** para habilitar la directiva. Desactive la casilla **Habilitada** para deshabilitar la directiva. El cuadro **Habilitada** se aplica a la automatización de las directivas. Crea o quita el sistema de automatización para la directiva. La automatización utiliza los mecanismos siguientes:  
  
 **Al cambiar: impedir**  
 Un desencadenador de base de datos exige la compatibilidad.  
  
 **Al cambiar: solo registro**  
 Un evento de servicios de notificación comprueba la compatibilidad.  
  
 **Al programar**  
 Se crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para comprobar la compatibilidad según una programación.  
  
 Con las directivas que se ejecutan utilizando el modo de evaluación **A petición** no se usa esta casilla.  
  
 **Condición de comprobación**  
 Seleccione la condición de la administración basada en directivas que esta directiva utiliza. Se enumeran todas las condiciones del servidor para la faceta de administración basada en directivas asociada. Haga clic en **Nueva condición** para crear una condición nueva. Haga clic en el botón de puntos suspensivos (**…**) para modificar la condición.  
  
 **Para destinos**  
 Seleccione los tipos de destino que están disponibles para que esta faceta complete una expresión de filtro.  
  
 **Modo de evaluación**  
 Seleccione el modo de evaluación para la directiva. Algunas directivas se pueden comprobar pero no exigir. Los modos de evaluación son los siguientes:  
  
 **A petición**  
 La directiva solo se ejecutará desde el cuadro de diálogo **Evaluar** .  
  
 **Al programar**  
 La directiva se evalúa periódicamente, se graba una entrada de registro para las directivas que no se cumplen y se crea un informe. Habilita el cuadro **Programación** .  
  
 **Al cambiar: solo registro**  
 Cuando se prueban los cambios, esta opción no evita los cambios que no cumplen la directiva, pero registra las infracciones de la directiva.  
  
 **Al cambiar: impedir**  
 Cuando se prueban los cambios, esta opción evita los cambios que infringirían la directiva.  
  
 **Programación**  
 Esta opción aparece cuando está seleccionado el modo de evaluación **Al programar** . Escriba el nombre de la programación, haga clic en **Seleccionar** para seleccionar una programación de una lista o haga clic en **Nueva** para crear una nueva. Para habilitar el área de programación, debe seleccionarse **Al programar** .  
  
 **Restricción de servidor**  
 Seleccione los tipos de servidores que son adecuados para esta directiva. Las opciones son **Ninguno** o seleccionar una condición que filtre los servidores posibles.  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
