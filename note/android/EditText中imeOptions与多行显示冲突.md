正常情况下，`EditText` 是会默认换行的，此时添加 `imeOptions` 属性是没有效果的。若增加 `singleLine` 属性为 `true`，则 `imeOptions` 功能正常。因此，默认情况下，对 `EditText` 来说，`imeOptions` 和多行显示是不兼容的。但是在很多实际应用中，这肯定是不行的。需要重写 EditText :

```
public class MultiSendEditText extends android.support.v7.widget.AppCompatEditText {


    public MultiSendEditText(Context context) {
        super(context);
    }

    public MultiSendEditText(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public MultiSendEditText(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    public InputConnection onCreateInputConnection(EditorInfo outAttrs) {
        InputConnection connection = super.onCreateInputConnection(outAttrs);

        int imeActions = outAttrs.imeOptions & EditorInfo.IME_MASK_ACTION;
        if ((imeActions & EditorInfo.IME_ACTION_SEND) != 0) {
            // clear the existing action
            outAttrs.imeOptions ^= imeActions;
            // set the DONE action
            outAttrs.imeOptions |= EditorInfo.IME_ACTION_SEND;
        }
        if ((outAttrs.imeOptions & EditorInfo.IME_FLAG_NO_ENTER_ACTION) != 0) {
            outAttrs.imeOptions &= ~EditorInfo.IME_FLAG_NO_ENTER_ACTION;
        }
        return connection;
    }
}
```

直接使用即可，无需再设置 `imeOptions` 属性。
