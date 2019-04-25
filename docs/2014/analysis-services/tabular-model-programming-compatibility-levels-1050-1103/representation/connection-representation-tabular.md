---
title: Representación de conexión (Tabular) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffd99068db329ea8e9066c6bd9508dc13f239690
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757766"
---
# <a name="connection-representation-tabular"></a>Representación de conexión (tabular)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  El objeto de conexión define el origen de datos que rellena el modelo tabular.  
  
## <a name="connection-representation"></a>Representación de conexión  
 La especificación del objeto de conexión sigue las reglas de los proveedores OLE DB.  
  
### <a name="connection-in-amo"></a>Conexión en AMO  
 Cuando se usa AMO para administrar una base de datos de modelo tabular, el objeto <xref:Microsoft.AnalysisServices.DataSource> en AMO coincide de forma unívoca con el objeto lógico de conexión.  
  
 En el fragmento de código siguiente se muestra cómo crear un objeto de conexión o un origen de datos de AMO en un modelo tabular.  
  
```  
  
//Create an OLEDB connection string  
StringBuilder SqlCnxStr = new StringBuilder();  
SqlCnxStr.Append(String.Format("Data Source={0};" ,SQLServer.Text));  
SqlCnxStr.Append(String.Format("Initial Catalog={0};", SQLDatabase.Text));  
SqlCnxStr.Append(String.Format("Persist Security Info={0};", false));  
SqlCnxStr.Append(String.Format("Integrated Security={0};", "SSPI"));  
SqlCnxStr.Append(String.Format("Provider={0}", "SQLNCLI11"));  
String DatasourceCnxString = SqlCnxStr.ToString();  
  
//Verify connection string and connectivity  
System.Data.OleDb.OleDbConnection OleDbCnx = new System.Data.OleDb.OleDbConnection(DatasourceCnxString);  
try  
{  
    OleDbCnx.Open();  
}  
catch ()  
{  
    throw;  
}  
String newDataSourceName = (string.IsNullOrEmpty(DataSourceName.Text) || string.IsNullOrWhiteSpace(DataSourceName.Text)) ? SQLDatabase.Text : DataSourceName.Text;  
AMO.DataSource newDatasource = newDatabase.DataSources.Add(newDataSourceName, newDataSourceName);  
newDatasource.ConnectionString = DatasourceCnxString.Text;  
if (impersonateServiceAccount.Checked)  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateServiceAccount);  
else  
{  
    if (String.IsNullOrEmpty(impersonateAccountUserName.Text))  
    {  
        MessageBox.Show(String.Format("Account User Name cannot be blank when using 'ImpersonateAccount' mode"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        return;  
    }  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateAccount, impersonateAccountUserName.Text, impersonateAccountPassword.Text);  
}  
newDatasource.Update();  
  
```  
  
## <a name="tabular-amo-2012-sample"></a>Ejemplo de AMO 2012 tabular  
 Para obtener una mejor comprensión acerca de cómo se usa AMO para crear y manipular representaciones de conexión, vea el código fuente del ejemplo AMO 2012 Tabular; en concreto, compruebe en el siguiente archivo fuente: Database.cs. El ejemplo está disponible en Codeplex. El código de ejemplo se proporciona únicamente como apoyo a los conceptos lógicos explicados aquí y no se debe usar en un entorno de producción.  
  
  
