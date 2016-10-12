# side-by-side-compare

##HTML
```
<div class="row">
  <div class="col-sm-6 mergeLeft">
      <div class="checkbox">
          <input name="checkL9" id="checkL9" class="check checkMe" type="checkbox">
          <label for="checkL9"><span class="boldMe">Profile Complete:</span>80%</label>
      </div>
  </div>
  <div class="col-sm-6 mergeRight">
      <div class="checkbox">
          <input name="checkR9" id="checkR9" class="check checkMe" type="checkbox">
          <label for="checkR9"><span class="boldMe">Profile Complete:</span>98%</label>
      </div>
  </div>
</div>
<div class="row">
  <div class="col-sm-6 mergeLeft">
      <div class="checkbox">
          <input name="checkL10" id="checkL10" class="check checkMe" type="checkbox">
          <label for="checkL10"><span class="boldMe">Profile ID:</span>54132132</label>
      </div>
  </div>
  <div class="col-sm-6 mergeRight">
      <div class="checkbox">
          <input name="checkR10" id="checkR10" class="check checkMe" type="checkbox">
          <label for="checkR10"><span class="boldMe">Profile ID:</span>8741328</label>
      </div>
  </div>
</div>
```

##Javascript
*set variables*
```
checkR9ID = (document.getElementById('checkR9'));
checkL9ID = (document.getElementById('checkL9'));
checkR10ID = (document.getElementById('checkR10'));
checkL10ID = (document.getElementById('checkL10'));
```

*create function*
```
function compareLR(a, b) {
    if (a.checked === true) {
        b.checked = false;            
    } else if (a.checked === false){
        b.checked = true;            
    }
}
```

*on click event of each radio button input, pass the declared values from the variables into the function*
```
//9th row
$('#checkR9').click(function () {
    compareLR(checkR9ID, checkL9ID);
});
$('#checkL9').click(function () {
    compareLR(checkL9ID, checkR9ID);
});
//10th row
$('#checkR10').click(function () {
    compareLR(checkR10ID, checkL10ID);
});
$('#checkL10').click(function () {
    compareLR(checkL10ID, checkR10ID);
});
```
