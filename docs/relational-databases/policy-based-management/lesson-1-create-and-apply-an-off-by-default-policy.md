---
title: 'Lección 1: Creación y aplicación de una directiva Desactivado de forma predeterminada'
description: Tutorial que le enseña a crear y aplicar una directiva Desactivado de forma predeterminada para la administración basada en directivas en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ea4b3c26cba886b5150b1bef7b8f3b08380c7a98
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892485"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>Lección 1: Creación y aplicación de una directiva Desactivado de forma predeterminada
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
El uso de directivas de administración basada en directivas permite administrar una o varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uno o varios objetos de instancia, instancias de servidor, una o varias bases de datos o uno o varios objetos de base de datos. Como administrador de bases de datos, debe asegurarse de que ciertos servidores no tienen habilitado Correo electrónico de base de datos. En esta lección, creará una condición y una directiva que establezca esa opción de servidor. Probará el servidor para ver si cumple con la directiva. A continuación, utilizará la directiva para volver a configurar el servidor de modo que cumpla con ella.  

## <a name="prerequisites"></a>Prerrequisitos
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio y acceso a un servidor que ejecute SQL Server. 

- Instale [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-mail-off-condition"></a>Creación de la condición Correo desactivado

1.  En el Explorador de objetos, expanda **Administración**, **Administración de directivas**y **Facetas**, haga clic con el botón derecho en **Configuración de área expuesta**y, después, haga clic en **Nueva condición**.  

    ![Nueva condición](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  En el cuadro de diálogo **Crear nueva condición** , en el cuadro **Nombre** , escriba **Correo desactivado**.   
    1. En el cuadro **Faceta** , confirme que está seleccionada la faceta **Configuración de área expuesta** .
    1. En el área **Expresión**, en el cuadro **Campo**, seleccione **\@DatabaseMailEnabled**, en el cuadro **Operador**, seleccione **=** y, en **Valor**, seleccione **False**.  
    1. En la página **Descripción** , escriba la descripción de la condición y luego haga clic en **Aceptar** para crear la condición.  

    ![Condición Correo desactivado](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>Creación de la directiva Desactivado de forma predeterminada  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en **Configuración de área expuesta**y, después, haga clic en **Nueva directiva**.  
  
2.  En el cuadro de diálogo **Crear nueva directiva** , en el cuadro **Nombre** , escriba **Desactivado de forma predeterminada**. 
    1. Deje desactivada la casilla **Habilitado** . La casilla **Habilitado** se aplica a las directivas automatizadas y esta directiva se ejecutará a petición.
    1. En la casilla **Condición de comprobación** , desplácese hacia abajo hasta el área **Configuración de área expuesta** y luego seleccione **Correo desactivado** como condición para comprobar.
    1. El cuadro **Para destinos** estará en blanco porque se trata de una directiva con ámbito de servidor. 
    1. En la casilla **Modo de evaluación** , seleccione **A petición** .
    1. En la casilla **Restricción de servidor** , seleccione **Ninguna**.
    1. En la página **Descripción** , escriba la descripción de la directiva.  

    ![Directiva Desactivado de forma predeterminada](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. En la página de descripción, puede proporcionar un hipervínculo a una página web para las directivas en el área **Hipervínculo de ayuda adicional** . En el cuadro **Texto para mostrar** , escriba el texto que aparecerá para el hipervínculo.
    1. En el cuadro **Dirección** , escriba un hipervínculo a una página de Ayuda, por ejemplo, la página principal del departamento de IT de la compañía.
    1. Para confirmar la dirección y abrir la página web, haga clic en **Probar vínculo**.
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Vínculo web de directiva Desactivado de forma predeterminada](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>Configuración de un servidor para ejecutar la directiva Desactivado de forma predeterminada 

1.  En el Explorador de objetos, haga clic con el botón derecho en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **Directivas**y haga clic en **Evaluar**.  

    ![evaluar directiva](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  En el cuadro de diálogo **Evaluar directivas** puede seleccionar las directivas de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de un archivo. Para este paso, deje **Origen** establecido en su instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
    1. En la sección **Directivas** , seleccione la directiva **Desactivado de forma predeterminada** .
    1. Para ver si el servidor cumple la directiva, haga clic en **Evaluar**.
    1. En el área **Resultados** , verá un círculo verde con una marca de verificación si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] cumple la directiva. Verá un círculo rojo con una X si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no cumple la directiva. 

   ![Evaluación de directiva Desactivar de forma predeterminada](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  En el área **Detalles del destino** , verá información adicional en la columna **Mensaje** si se produce un error. En la columna **Mensaje** , haga clic en **Ver** para ver un informe que contiene los resultados de la comprobación de cada propiedad de faceta que se comprobó. 

    ![Visualización los resultados de evaluación de la directiva](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  La descripción de la directiva se muestra en la parte inferior de la página y la sección **Ayuda adicional** muestra el hipervínculo que ha configurado para la directiva. Haga clic en el hipervínculo de mensaje para abrir la página web que especificó al crear la directiva.   

1.  Cierre el explorador y, después, cierre el cuadro de diálogo **Vista detallada de resultados** .  

1. Si el servidor no cumple la directiva y quiere deshabilitar Correo electrónico de base de datos, haga clic en **Aplicar** en la página **Resultados de la evaluación** .  
  
10. Cierre los cuadros de diálogo **Vista detallada de resultados** y **Evaluar directivas** .   

   
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Creación y aplicación de una directiva de normas de denominación](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
