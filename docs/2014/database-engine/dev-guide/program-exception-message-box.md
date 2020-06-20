---
title: Cuadro de mensajes de excepción de programa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 52fc203075b06485c89fe4d2d3149472c57719f9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933412"
---
# <a name="program-exception-message-box"></a>Programar cuadros de mensajes de excepción
  Puede usar el cuadro de mensajes de excepción en sus aplicaciones para proporcionar un control considerablemente mayor sobre la experiencia de mensajería que el que se proporciona con la clase <xref:System.Windows.Forms.MessageBox>. Para obtener más información, vea [programación de cuadros de mensajes de excepción](../../../2014/database-engine/dev-guide/exception-message-box-programming.md). Para obtener información sobre la forma de obtener e implementar el archivo .dll del cuadro de mensajes de excepción, vea [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md).  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>Para controlar una excepción mediante el cuadro de mensajes de excepción  
  
1.  Agregue una referencia al ensamblado Microsoft.ExceptionMessageBox.dll en su proyecto de código administrado.  
  
2.  Opta Agregue una `using` Directiva (C#) o `Imports` ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .net) para usar el <xref:Microsoft.SqlServer.MessageBox> espacio de nombres.  
  
3.  Cree un bloque try-catch para controlar la excepción anticipada.  
  
4.  Dentro del bloque `catch`, cree una instancia de la clase <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>. Pase el <xref:System.Exception> objeto controlado por el `try` - `catch` bloque.  
  
5.  (Opcional) Establezca una o varias de las siguientes propiedades en <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons>enumeración que especifica los botones que se van a mostrar en el cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton>enumeración que especifica el botón predeterminado para el cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions>enumeración que se utiliza para controlar otros comportamientos del cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol>enumeración que especifica el símbolo que se va a mostrar en el cuadro de mensaje de excepción.  
  
6.  Llame al método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A>. Pase la ventana primaria a la que pertenece el cuadro de mensajes de excepción.  
  
7.  Opta Tenga en cuenta el valor de la <xref:System.Windows.Forms.DialogResult> enumeración devuelta si necesita determinar en qué botón hizo clic el usuario.  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>Para mostrar el cuadro de mensajes de excepción sin una excepción  
  
1.  Agregue una referencia al ensamblado Microsoft.ExceptionMessageBox.dll en su proyecto de código administrado.  
  
2.  Opta Agregue una `using` Directiva (C#) o `Imports` (Visual Basic .net) para usar el <xref:Microsoft.SqlServer.MessageBox> espacio de nombres.  
  
3.  Cree una instancia de la clase <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>. Pase el texto del mensaje como un valor <xref:System.String>.  
  
4.  (Opcional) Establezca una o varias de las siguientes propiedades en <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons>enumeración que especifica los botones que se van a mostrar en el cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A>: título del cuadro de diálogo del cuadro de mensajes de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton>enumeración que especifica el botón predeterminado del cuadro de diálogo del cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions>enumeración que se utiliza para controlar otros comportamientos del cuadro de mensaje de excepción.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol>enumeración que especifica el símbolo que se va a mostrar en el cuadro de mensaje de excepción.  
  
5.  Llame al método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A>. Pase la ventana primaria a la que pertenece el cuadro de mensajes de excepción.  
  
6.  (Opcional) Tenga en cuenta el valor de la enumeración <xref:System.Windows.Forms.DialogResult> devuelta si necesita determinar en qué botón ha hecho clic el usuario.  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>Para mostrar el cuadro de mensajes de excepción con botones personalizados  
  
1.  Agregue una referencia al ensamblado Microsoft.ExceptionMessageBox.dll en su proyecto de código administrado.  
  
2.  Opta Agregue una `using` Directiva (C#) o `Imports` (Visual Basic .net) para usar el <xref:Microsoft.SqlServer.MessageBox> espacio de nombres.  
  
3.  Cree una instancia de la clase <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> de una de estas dos formas:  
  
    -   Pase el <xref:System.Exception> objeto controlado por un `try` - `catch` bloque.  
  
    -   Pase el texto del mensaje como un valor <xref:System.String>.  
  
4.  Establezca uno de los siguientes valores para <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore>: muestra los botones **anular**, **Reintentar**y **omitir** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom>: muestra los botones personalizados.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK>: muestra el botón **Aceptar** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel>: muestra los botones **Aceptar** y **Cancelar** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel>-muestra los botones **Reintentar** y **Cancelar** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo>: muestra los botones **sí** y **no** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel>: muestra los botones **sí**, **no**y **Cancelar** .  
  
5.  (Opcional) Si usa botones personalizados, llame a una de las sobrecargas del método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> para especificar el texto para un máximo de cinco botones personalizados.  
  
6.  Llame al método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A>. Pase la ventana primaria a la que pertenece el cuadro de mensajes de excepción.  
  
7.  (Opcional) Tenga en cuenta el valor de la enumeración <xref:System.Windows.Forms.DialogResult> devuelta si necesita determinar en qué botón ha hecho clic el usuario. Si usa botones personalizados, tenga en cuenta el valor de <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> para que la propiedad <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> determine en cuál de los botones personalizados ha hecho clic el usuario.  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>Para permitir que los usuarios decidan si desean mostrar el cuadro de mensajes de excepción  
  
1.  Agregue una referencia al ensamblado Microsoft.ExceptionMessageBox.dll en su proyecto de código administrado.  
  
2.  Opta Agregue una `using` Directiva (C#) o `Imports` (Visual Basic .net) para usar el <xref:Microsoft.SqlServer.MessageBox> espacio de nombres.  
  
3.  Cree una instancia de la clase <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> de una de estas dos formas:  
  
    -   Pase el <xref:System.Exception> objeto controlado por un `try` - `catch` bloque.  
  
    -   Pase el texto del mensaje como un valor <xref:System.String>.  
  
4.  Establezca la propiedad <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> en `true`.  
  
5.  (Opcional) Especifique el texto donde se solicita al usuario que decida si desea que se muestre de nuevo el cuadro de mensajes de excepción para <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>. El texto predeterminado es "No volver a mostrar este mensaje".  
  
6.  Si necesita mantener la decisión del usuario solamente durante la ejecución de la aplicación, establezca el valor de <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> en una variable <xref:System.Boolean> global. Evalúe este valor antes de crear una instancia del cuadro de mensajes de excepción.  
  
7.  Si necesita almacenar la decisión de un usuario de manera permanente, haga lo siguiente:  
  
    1.  Llame al método CreateSubKey para abrir una clave del Registro personalizada utilizada por la aplicación y establezca <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> en el objeto RegistryKey devuelto.  
  
    2.  Establezca <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> en el nombre del valor del Registro utilizado.  
  
    3.  Establezca <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> en `true`.  
  
    4.  Llame al método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A>. Se evalúa la clave del Registro especificada y solamente se muestra el cuadro de mensajes de excepción si los datos almacenados en la clave del Registro son iguales a 0. Si se muestra el cuadro de diálogo y el usuario activa la casilla antes de hacer clic en un botón, los datos de la clave del Registro se establecen en 1.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, el cuadro de mensajes de excepción se usa solamente con el botón **Aceptar** para mostrar información de una excepción de la aplicación que incluye la excepción controlada junto con información adicional específica de la aplicación.  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa el cuadro de mensajes de excepción con los botones **Sí** y **No** entre los que debe elegir el usuario.  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa el cuadro de mensajes de excepción con botones personalizados.  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa la casilla para determinar si debe mostrarse el cuadro de mensajes de excepción.  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa la casilla y una clave del Registro para determinar si debe mostrarse el cuadro de mensajes de excepción.  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa el cuadro de mensajes de excepción para mostrar información adicional que puede resultar de utilidad para la depuración o solución de problemas.  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
