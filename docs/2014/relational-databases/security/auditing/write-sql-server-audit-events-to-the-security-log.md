---
title: Escribir eventos de auditoría de SQL Server en el registro de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e9beeacd905235bb268d0f4a3f6fbca8a291dccf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201125"
---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>Escribir eventos de auditoría de SQL Server en el registro de seguridad
  En un entorno de alta seguridad, el registro de seguridad de Windows es la ubicación adecuada para escribir los eventos que registran el acceso a los objetos. Se admiten otras ubicaciones de auditoría pero están más expuestas a alteraciones.  
  
 Hay dos requisitos clave para escribir las auditorías del servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el registro de seguridad de Windows:  
  
-   El valor Auditar el acceso a objetos se debe configurar para capturar los eventos. La herramienta de directiva de auditoría (`auditpol.exe`) expone diversos valores de subdirectivas en la categoría **Auditar el acceso a objetos** . Para permitir que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] audite el acceso a los objetos, configure el valor **Aplicación generada** .  
  
-   La cuenta en la que el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se esté ejecutando debe tener el permiso **Generar auditorías de seguridad** para escribir en el registro de seguridad de Windows. De forma predeterminada, las cuentas LOCAL SERVICE y NETWORK SERVICE tienen este permiso. No se requiere este paso si [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se está ejecutando en alguna de esas cuentas.  
  
 La directiva de auditoría de Windows puede afectar a la auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si se configura para escribir en el registro de seguridad de Windows, con la posibilidad de perder eventos si la directiva de auditoría se configura incorrectamente. Por lo general, el registro de seguridad de Windows se establece para sobrescribir los eventos más antiguos. De esta forma se conservan los eventos más recientes. Sin embargo, si el registro de seguridad de Windows no se establece para sobrescribir los eventos más antiguos, entonces, si el registro de seguridad se llena, el sistema emitirá el evento 1104 de Windows (el registro está lleno). En ese punto:  
  
-   No se registrará ningún evento de seguridad más  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no podrá detectar que el sistema no puede grabar eventos en el registro de seguridad, lo que provoca la posible pérdida de eventos de auditoría  
  
-   Después de que el administrador corrija el registro de seguridad, el comportamiento de registro volverá a la normalidad.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para escribir eventos de auditoría de SQL Server en el registro de seguridad:**  
  
     [Configurar el valor Auditar el acceso a objetos en Windows utilizando auditpol](#auditpolAccess)  
  
     [Configurar el valor Auditar el acceso a objetos en Windows utilizando secpol](#secpolAccess)  
  
     [Conceder el permiso Generar auditorías de seguridad a una cuenta utilizando secpol](#secpolPermission)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Los administradores del equipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deberían saber que una directiva de dominio puede sobrescribir la configuración regional del registro de seguridad. En este caso, la directiva de dominio puede sobrescribir el valor de subcategoría (**auditpol /get /subcategory:"aplicación generada"**). Esto puede afectar a la capacidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de registrar los eventos sin que haya ninguna manera de detectar que los eventos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está intentando auditar no van a ser grabados.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe ser administrador de Windows para configurar estos valores.  
  
##  <a name="auditpolAccess"></a> Para configurar el valor Auditar el acceso a objetos en Windows utilizando auditpol  
  
1.  Abra un símbolo del sistema con permisos administrativos.  
  
    1.  En el menú **Inicio** , seleccione **Todos los programas**, **Accesorios**, haga clic con el botón derecho en **Símbolo del sistema**y, después, haga clic en **Ejecutar como administrador**.  
  
    2.  Si se abre el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Continuar**.  
  
2.  Ejecute la instrucción siguiente para habilitar la auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  Cierre la ventana del símbolo del sistema.  
  
##  <a name="secpolAccess"></a> Para conceder el permiso Generar auditorías de seguridad a una cuenta utilizando secpol  
  
1.  En cualquier sistema operativo Windows, en el menú **Inicio** , haga clic en **Ejecutar**.  
  
2.  Escriba **secpol.msc** y, a continuación, haga clic en **Aceptar**. Si aparece el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Continuar**.  
  
3.  En la herramienta Directiva de seguridad local, expanda **Configuración de seguridad**, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
4.  En el panel de resultados, haga doble clic en **Generar auditorías de seguridad**.  
  
5.  En la pestaña **Configuración de seguridad local** , haga clic en **Agregar usuario o grupo**.  
  
6.  En el cuadro de diálogo **Seleccionar usuarios, equipos o grupos** , escriba el nombre de la cuenta de usuario, como **domain1\user1** y, después, haga clic en **Aceptar**, o haga clic en **Opciones avanzadas** y busque la cuenta.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  Cierre la herramienta Directiva de seguridad.  
  
9. Reinicie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para habilitar este valor.  
  
##  <a name="secpolPermission"></a> Para configurar el valor Auditar el acceso a objetos en Windows utilizando secpol  
  
1.  Si el sistema operativo es anterior a [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] o Windows Server 2008, en el menú **Inicio** , haga clic en **Ejecutar**.  
  
2.  Escriba **secpol.msc** y, a continuación, haga clic en **Aceptar**. Si aparece el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Continuar**.  
  
3.  En la herramienta Directiva de seguridad local, expanda **Configuración de seguridad**, expanda **Directivas locales**y, a continuación, haga clic en **Directiva de auditoría**.  
  
4.  En el panel de resultados, haga doble clic en **Auditar el acceso a objetos**.  
  
5.  En la pestaña **Configuración de seguridad local** , en el área **Auditar estos intentos** , seleccione **Correcto** y **Error**.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Cierre la herramienta Directiva de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Audit &#40;motor de base de datos&#41;](sql-server-audit-database-engine.md)  
  
  