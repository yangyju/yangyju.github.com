---
layout: post
title: DoModal() return -1 && ActiveX Control
---
Maybe you have disabled the ActiveX Control Fuction when you create the MFC App. 

If you want to use ActiveX Control later,

add 
```CPP
AfxEnableControlContainer();
```
like this

```CPP
BOOL CDemoApp::InitInstance()
{
	// Standard initialization
	// If you are not using these features and wish to reduce the size
	//  of your final executable, you should remove from the following
	//  the specific initialization routines you do not need.

	AfxEnableControlContainer();

	CDemoDlg dlg;
	m_pMainWnd = &dlg;
	int nResponse = dlg.DoModal();


```
or -1 is return when call dlg.DoModal().