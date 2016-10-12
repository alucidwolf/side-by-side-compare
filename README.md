# side-by-side-compare

Say you want to compare profile information side by side, and then submit the info that is in the checkbox to create a new profile from the two current profiles whose information you chose to keep from each individual profile.

Below is some bootstrapped HTML and some javascript that will toggle off/on the checkbox for the item adjacent to the item clicked. See example below. If you click on/off one of the checkboxes, the other one in the row will toggle accoridngly so only 1 is checked at a time.

![alt text](http://i1295.photobucket.com/albums/b638/b2_franklin/compare%20profile_zpsofujeesa.jpg "Example")

##HTML
*for the input fields*
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

*for the button that triggers the preview modal*
```
<button type="button" onclick="getLabelText()" class="btn btn-primary" data-toggle="modal" data-target="#manualMergeReviewModal">Review &amp; Merge</button>
```

*for the actual modal that has the container which puts values of the checked checkboxes into it*
```
<div class="modal fade" id="manualMergeReviewModal" role="dialog" aria-labelledby="manualMergeReviewModalLabel">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-body">
                <div class="container-fluid">
                    <div id="mergeCompare" class="row">

                        @*this is where the text for the checked labels is being copied for user to review  before submitting*@

                    </div>
                    <div class="prev">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal" aria-label="Close">I need to make more changes</button>
                    </div>
                    <div class="next">
                        <button type="submit" class="btn btn-primary">Merge!</button>
                    </div>
                </div>                        
            </div>
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

*then, if you want to create a button to popup a modal that displays the info the user has checked before submitting the Merge request, you can do that with this function call on the button click event*
```
function getLabelText() {
    if ($('.mmReviewSingle').length > 0) {
        $('.mmReviewSingle').remove();
    }
    var array = [];    
    array = $('#manualMerge input:checked').next('label').map(function () {
        return $(this).text();
    }).get();
    
    var mergeCompare = document.getElementById('mergeCompare');
    for (var i = 0; i < array.length; i++) {
        console.log(array[i]);
        var div = document.createElement('div');
        div.setAttribute('class', 'mmReviewSingle col-xs-12')
        div.innerHTML = (array[i]);
        mergeCompare.appendChild(div);
    }    
};
```
