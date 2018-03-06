# UI-grid

angularJs 网格插件



```javascript
$scope.gridOptions={
  	enableSorting:false, //禁用列级别排序  默认true
  	enableFiltering:false, //禁用列级筛选。 默认false
  	enableGridMenu:false,  //禁用网格菜单
  	enableColumnResizing:false, //调整列大小。 也可以配置单个def。  需要引用ui-grid-resize-column指令
  	rowEditWaitInterval:-1,	//如果设置为-1，则保存永远不会被定时器触发	
  
  
  //限制选择函数
  isRowSelectable：function(row){
    
  },
  
    columnDefs:[
		{
  			name:'列名',
  			field:'字段值',
  			cellFilter:'map',  //过滤器
             pinnedLeft:true,	//列固定
          
          	//编辑
          	enableCellEdit:false,	//禁止编辑  默认true
          	type:'number,string',	//提供编辑的默认编辑器分别为数字或布尔值或日期编辑器。
            editDropdownOptionsArray:[	//如果下拉列表需要填充一个数组值，默认情况下这些值应该是
              {id:xxx,value:xxx},
              {id:xxx,value:xxx}
            ],
            editDropdownOptionsFunction：function(rowEntity,colDef){	//可以代替上面的editArray
				//返回一个数组
            },
          	editableCellTemplate ：'ui-grid / dropdownEditor'，	
            editDropdownIdLabel:'xxx',
            editDropdownValueLabel:'xxx',
            editDropdownRowEntityOptionsArrayPath:xxx,
            editDropdownOptionsFunction:xxx,
  
  			//提示工具,当用户悬停在一个单元格上时弹出。
              cellTooltip:function(row,col){
				return '提示信息'
              },
  			cellHeaderTooltip:true //同上    支持cellFilter

  
  			//设置列的颜色
  			cellClass:function(grid,row,col,rowRenderIndex,colRenderIndex){
  				//dosomething
			}，
      
              headerCellClass:function(){
                //同上
              }
		}
    ]
    
    
    onRegisterApi:function(gridApi){
       $scope.gridApi = gridApi;
      
      
      //添加一个自定义列
      $scope.gridApi.core.addRowHeaderColumn({
        name:'rowHeaderCol',
        displayName:'',
        width:30,
        cellTemplate:'ui-grid/selectionRowHeader',//也可以用自己的template '<div>点击</div>'
      })
      
      
      
      //清空脏值
      var gridRows = $scope.gridApi.rowEdit.getDirtyRows();
	  var dataRows = gridRows.map( function( gridRow ) { return gridRow.entity; });
      $scope.gridApi.rowEdit.setRowsClean( dataRows );
      
      
      //获取改动的数据
      $scope.gridApi.rowEdit.getDirtyRows();
        
      //获取选中的数据
      $scope.gridApi.selection.getSelectedRows();
	 //清空复选框
	  $scope.gridApi.selection.clearSelectedRows();
      
    }
  
}
```







## API

### enableSorting   boolean

允许对进行排序默认true



### enableFiltering  boolean

是否开启过滤，默认false



