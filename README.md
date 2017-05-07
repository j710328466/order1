# sorting algorithm

    const oForm = document.getElementById('number_form');
    const oNumInput = document.getElementById('numberInput');
    const sortBtn = document.getElementById('sortBtn');
    const oMsg = document.querySelector('.bg-primary');
    let gNum = 1;
    const numArr = [];
    const arr = [];
    const orderedArr = [];
    // 11个桶子， 下标的，排序是现成的
    for (var i = 0; i < 11; i++) {
      // 桶子里都是空的
      arr[i] = 0;
    }
    oForm.addEventListener('submit', function(event){
      // 阻止预先关联的默认动作
      event.preventDefault();
      // trim string类型的一个方法， 去除左右的空格
      const num = oNumInput.value.trim();
      // 安全性检测
      // num 表单  string类型  parseInt  将字符串变数字
      if (num.length > 0 || !isNaN(num)) {
        if (gNum == 1) {
            document.querySelector('tbody').innerHTML = getTrHtml(num);
        } else {
            document.querySelector('tbody').innerHTML += getTrHtml(num);
        }
        numArr.push(parseInt(num));
        gNum++;
        // 除去输入框中的值
        oNumInput.value = '';
      } else {
        alert('请输入数字！');
      }
      // alert(num.length);
      // getTrHtml(num);
    });
    // 功能：提供新的一行/
    // 1 序号 从1增
    // 2 用户在表单中填的值
    // 3 返回tr html
    // 需要传参数，用户输入的
    function getTrHtml(num) {
      const str = `
      <tr>
        <td>${gNum}</td>
        <td>${num}</td>
      </tr>
      `;
      return str;
    }
    // 考试完， 要将同学们的成绩进行排序
    // 5分 3分 5分 2分 9分
    // 分数从小到大
    // 数组 桶排序 11 个数组的排序 0-10 分
    sortBtn.addEventListener('click',function(){
      // 1`获取当前用户输入的数据
      // console.log(numArr);
      for (let i = 0; i < numArr.length; i++) {
        // numArr[0] = 5 标签 5 两次
        arr[numArr[i]]++;
      }
      // console.log(arr);
      for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr[i]; j++) {
          orderedArr.push(i);
        }
      }
      oMsg.innerHTML = `从小到大排序：${orderedArr.join(',')}`;
    // 方法二
    // console.log(numArr.sort(function(a,b){
    //   return a > b;
    // }));
    });
