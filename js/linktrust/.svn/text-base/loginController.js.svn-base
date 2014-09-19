$.ready(function()
{
	doLogin = function() {
	var account = document.getElementById("username").value;
	var password = document.getElementById('password').value;
	if(!account)
	{
		$.alert("用户名不能为空!",'错误提示','确定',null);
		return;
	}
	if(!password)
	{
		$.alert("密码不能为空!",'错误提示','确定',null);
		return;
	}
	params = "?account="+account+"&password="+password;
	var url = LConstant.WEB + "/m/sys/login"+params;
	console.log(url);
	
	linktrust.jsonpAjax(url,LConstant.GET,function(data){
		if(!data.success)
		{
			$.alert(data.msg,'登陆失败','确定', null);
		}
	}, null);
};

document.getElementById("btnLogin").addEventListener('click',function(){
	doLogin();	
});
});



//document.on('click','#btnLogin', 'doLogin()');
