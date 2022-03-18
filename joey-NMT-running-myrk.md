# Joey-NMT Running with Myanmar-Rakhine Parallel Data

Joey-NMT ကို ကိုယ်ဒေတာနဲ့ကိုယ် run တတ်အောင် ဥပမာအနေနဲ့ run ပြထား...  

လောလောဆယ် joey-nmt ရဲ့ RNN မော်ဒယ်နဲ့ MT performance ကို ကြည့်ကြည့်မယ်...  
အချိန်ဘယ်လောက် ကြာမယ် ဆိုတာကိုလည်း သိချင်တယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/small.myrk.yaml 
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 16:56:01,610 - INFO - joeynmt.training - Epoch   1, Step:     1160, Batch Loss:     3.408352, Tokens per Sec:      834, Lr: 0.000156
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #0
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #1
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #2
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     1160: bleu:   0.00, loss: 3581.4941, ppl:   1.3005, duration: 6.5147s
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 16:56:08,866 - INFO - joeynmt.training - Training ended since minimum lr 0.0001 was reached.
2022-02-26 16:56:08,867 - INFO - joeynmt.training - Best validation result (greedy) at step     1040: 3579.62 loss.
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/1040.ckpt
2022-02-26 16:56:08,886 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 16:56:08,889 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 16:56:08,890 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.dev
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 16:56:44,886 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:44,887 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.test

real	18m17.359s
user	118m39.958s
sys	2m28.652s

```

၁၈ မိနစ်ခန့်ပဲ ကြာတယ်။  

## Testing with RNN Model for My-RK

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt translate configs/small.myrk.yaml < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./models/small_model_myrk/myrk.syl.out
2022-02-26 17:06:02,582 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:06:02,611 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 17:06:02,615 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:06:02,618 - INFO - joeynmt.model - Enc-dec model built.

real	0m20.380s
user	2m20.991s
sys	0m0.875s
(joey) ye@:~/exp/joeynmt$
```

### Check the Log Files

```
2022-02-26 16:56:08,731 - DEBUG - matplotlib.backends.backend_pdf - Writing TrueType font.
2022-02-26 16:56:08,866 - INFO - joeynmt.training - Training ended since minimum lr 0.0001 was reached.
2022-02-26 16:56:08,867 - INFO - joeynmt.training - Best validation result (greedy) at step     1040: 3579.62 loss.
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/1040.ckpt
2022-02-26 16:56:08,886 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 16:56:08,889 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 16:56:08,890 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.dev
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 16:56:44,886 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:44,887 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.test
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$ cat ./validations.txt 
Steps: 10	Loss: 63616.55078	PPL: 106.45625	bleu: 0.00000	LR: 0.00500000	*
Steps: 20	Loss: 26462.26172	PPL: 6.96999	bleu: 0.00000	LR: 0.00500000	*
Steps: 30	Loss: 6819.06641	PPL: 1.64927	bleu: 0.00000	LR: 0.00500000	*
Steps: 40	Loss: 4358.31396	PPL: 1.37683	bleu: 0.00000	LR: 0.00500000	*
Steps: 50	Loss: 3905.57471	PPL: 1.33184	bleu: 0.00000	LR: 0.00500000	*
Steps: 60	Loss: 3798.10986	PPL: 1.32138	bleu: 0.00000	LR: 0.00500000	*
Steps: 70	Loss: 3683.61304	PPL: 1.31033	bleu: 0.00000	LR: 0.00500000	*
Steps: 80	Loss: 3674.39038	PPL: 1.30944	bleu: 0.00000	LR: 0.00500000	*
Steps: 90	Loss: 3664.30811	PPL: 1.30847	bleu: 0.00000	LR: 0.00500000	*
Steps: 100	Loss: 3639.98413	PPL: 1.30614	bleu: 0.00000	LR: 0.00500000	*
Steps: 110	Loss: 3637.31250	PPL: 1.30588	bleu: 0.00000	LR: 0.00500000	*
Steps: 120	Loss: 3627.07373	PPL: 1.30490	bleu: 0.00000	LR: 0.00500000	*
Steps: 130	Loss: 3622.11011	PPL: 1.30443	bleu: 0.00000	LR: 0.00500000	*
Steps: 140	Loss: 3617.94604	PPL: 1.30403	bleu: 0.00000	LR: 0.00500000	*
Steps: 150	Loss: 3617.85791	PPL: 1.30402	bleu: 0.00000	LR: 0.00500000	*
Steps: 160	Loss: 3613.80103	PPL: 1.30363	bleu: 0.00000	LR: 0.00500000	*
Steps: 170	Loss: 3608.61084	PPL: 1.30314	bleu: 0.00000	LR: 0.00500000	*
Steps: 180	Loss: 3605.76758	PPL: 1.30287	bleu: 0.00000	LR: 0.00500000	*
Steps: 190	Loss: 3604.20532	PPL: 1.30272	bleu: 0.00000	LR: 0.00500000	*
Steps: 200	Loss: 3611.28711	PPL: 1.30339	bleu: 0.00000	LR: 0.00500000	
Steps: 210	Loss: 3601.01953	PPL: 1.30241	bleu: 0.00000	LR: 0.00500000	*
Steps: 220	Loss: 3609.77881	PPL: 1.30325	bleu: 0.00000	LR: 0.00500000	
Steps: 230	Loss: 3597.10034	PPL: 1.30204	bleu: 0.00000	LR: 0.00500000	*
Steps: 240	Loss: 3595.85669	PPL: 1.30192	bleu: 0.00000	LR: 0.00500000	*
Steps: 250	Loss: 3605.42236	PPL: 1.30283	bleu: 0.00000	LR: 0.00500000	
Steps: 260	Loss: 3596.00537	PPL: 1.30193	bleu: 0.00000	LR: 0.00500000	
Steps: 270	Loss: 3598.31812	PPL: 1.30215	bleu: 0.00000	LR: 0.00500000	
Steps: 280	Loss: 3591.86255	PPL: 1.30154	bleu: 0.00000	LR: 0.00500000	*
Steps: 290	Loss: 3591.77832	PPL: 1.30153	bleu: 0.00000	LR: 0.00500000	*
Steps: 300	Loss: 3590.96387	PPL: 1.30145	bleu: 0.00000	LR: 0.00500000	*
Steps: 310	Loss: 3590.57886	PPL: 1.30141	bleu: 0.00000	LR: 0.00500000	*
Steps: 320	Loss: 3598.61182	PPL: 1.30218	bleu: 0.00000	LR: 0.00500000	
Steps: 330	Loss: 3604.26172	PPL: 1.30272	bleu: 0.00000	LR: 0.00500000	
Steps: 340	Loss: 3587.80713	PPL: 1.30115	bleu: 0.00000	LR: 0.00500000	*
Steps: 350	Loss: 3587.35400	PPL: 1.30111	bleu: 0.00000	LR: 0.00500000	*
Steps: 360	Loss: 3591.36426	PPL: 1.30149	bleu: 0.00000	LR: 0.00500000	
Steps: 370	Loss: 3586.71948	PPL: 1.30105	bleu: 0.00000	LR: 0.00500000	*
Steps: 380	Loss: 3587.64160	PPL: 1.30113	bleu: 0.00000	LR: 0.00500000	
Steps: 390	Loss: 3586.05933	PPL: 1.30098	bleu: 0.00000	LR: 0.00500000	*
Steps: 400	Loss: 3588.46240	PPL: 1.30121	bleu: 0.00000	LR: 0.00500000	
Steps: 410	Loss: 3591.14600	PPL: 1.30147	bleu: 0.00000	LR: 0.00500000	
Steps: 420	Loss: 3584.80835	PPL: 1.30086	bleu: 0.00000	LR: 0.00500000	*
Steps: 430	Loss: 3584.30103	PPL: 1.30081	bleu: 0.00000	LR: 0.00500000	*
Steps: 440	Loss: 3584.98682	PPL: 1.30088	bleu: 0.00000	LR: 0.00500000	
Steps: 450	Loss: 3587.60474	PPL: 1.30113	bleu: 0.00000	LR: 0.00500000	
Steps: 460	Loss: 3586.50366	PPL: 1.30102	bleu: 0.00000	LR: 0.00500000	
Steps: 470	Loss: 3585.23682	PPL: 1.30090	bleu: 0.00000	LR: 0.00500000	
Steps: 480	Loss: 3589.81104	PPL: 1.30134	bleu: 0.00000	LR: 0.00500000	
Steps: 490	Loss: 3582.60669	PPL: 1.30065	bleu: 0.00000	LR: 0.00500000	*
Steps: 500	Loss: 3584.86279	PPL: 1.30087	bleu: 0.00000	LR: 0.00500000	
Steps: 510	Loss: 3582.95288	PPL: 1.30069	bleu: 0.00000	LR: 0.00500000	
Steps: 520	Loss: 3582.91504	PPL: 1.30068	bleu: 0.00000	LR: 0.00500000	
Steps: 530	Loss: 3585.79395	PPL: 1.30096	bleu: 0.00000	LR: 0.00500000	
Steps: 540	Loss: 3583.24780	PPL: 1.30071	bleu: 0.00000	LR: 0.00500000	
Steps: 550	Loss: 3607.86914	PPL: 1.30307	bleu: 0.00000	LR: 0.00250000	
Steps: 560	Loss: 3581.30029	PPL: 1.30053	bleu: 0.00000	LR: 0.00250000	*
Steps: 570	Loss: 3582.43359	PPL: 1.30064	bleu: 0.00000	LR: 0.00250000	
Steps: 580	Loss: 3582.40527	PPL: 1.30063	bleu: 0.00000	LR: 0.00250000	
Steps: 590	Loss: 3581.04492	PPL: 1.30050	bleu: 0.00000	LR: 0.00250000	*
Steps: 600	Loss: 3583.27319	PPL: 1.30072	bleu: 0.00000	LR: 0.00250000	
Steps: 610	Loss: 3583.37524	PPL: 1.30073	bleu: 0.00000	LR: 0.00250000	
Steps: 620	Loss: 3585.72192	PPL: 1.30095	bleu: 0.00000	LR: 0.00250000	
Steps: 630	Loss: 3581.77051	PPL: 1.30057	bleu: 0.00000	LR: 0.00250000	
Steps: 640	Loss: 3593.86060	PPL: 1.30173	bleu: 0.00000	LR: 0.00250000	
Steps: 650	Loss: 3586.39160	PPL: 1.30101	bleu: 0.00000	LR: 0.00125000	
Steps: 660	Loss: 3580.96167	PPL: 1.30050	bleu: 0.00000	LR: 0.00125000	*
Steps: 670	Loss: 3587.34399	PPL: 1.30111	bleu: 0.00000	LR: 0.00125000	
Steps: 680	Loss: 3581.25903	PPL: 1.30052	bleu: 0.00000	LR: 0.00125000	
Steps: 690	Loss: 3580.80737	PPL: 1.30048	bleu: 0.00000	LR: 0.00125000	*
Steps: 700	Loss: 3580.80493	PPL: 1.30048	bleu: 0.00000	LR: 0.00125000	*
Steps: 710	Loss: 3583.26343	PPL: 1.30072	bleu: 0.00000	LR: 0.00125000	
Steps: 720	Loss: 3583.63428	PPL: 1.30075	bleu: 0.00000	LR: 0.00125000	
Steps: 730	Loss: 3580.36914	PPL: 1.30044	bleu: 0.00000	LR: 0.00125000	*
Steps: 740	Loss: 3580.51953	PPL: 1.30045	bleu: 0.00000	LR: 0.00125000	
Steps: 750	Loss: 3588.47485	PPL: 1.30121	bleu: 0.00000	LR: 0.00125000	
Steps: 760	Loss: 3580.10107	PPL: 1.30041	bleu: 0.00000	LR: 0.00125000	*
Steps: 770	Loss: 3580.17139	PPL: 1.30042	bleu: 0.00000	LR: 0.00125000	
Steps: 780	Loss: 3590.39038	PPL: 1.30140	bleu: 0.00000	LR: 0.00125000	
Steps: 790	Loss: 3580.57349	PPL: 1.30046	bleu: 0.00000	LR: 0.00125000	
Steps: 800	Loss: 3580.10400	PPL: 1.30041	bleu: 0.00000	LR: 0.00125000	
Steps: 810	Loss: 3581.50732	PPL: 1.30055	bleu: 0.00000	LR: 0.00125000	
Steps: 820	Loss: 3580.26855	PPL: 1.30043	bleu: 0.00000	LR: 0.00062500	
Steps: 830	Loss: 3581.93774	PPL: 1.30059	bleu: 0.00000	LR: 0.00062500	
Steps: 840	Loss: 3580.07007	PPL: 1.30041	bleu: 0.00000	LR: 0.00062500	*
Steps: 850	Loss: 3579.92676	PPL: 1.30040	bleu: 0.00000	LR: 0.00062500	*
Steps: 860	Loss: 3579.88745	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	*
Steps: 870	Loss: 3581.90942	PPL: 1.30059	bleu: 0.00000	LR: 0.00062500	
Steps: 880	Loss: 3580.43994	PPL: 1.30045	bleu: 0.00000	LR: 0.00062500	
Steps: 890	Loss: 3579.80542	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	*
Steps: 900	Loss: 3579.78125	PPL: 1.30038	bleu: 0.00000	LR: 0.00062500	*
Steps: 910	Loss: 3579.90088	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	
Steps: 920	Loss: 3581.22998	PPL: 1.30052	bleu: 0.00000	LR: 0.00062500	
Steps: 930	Loss: 3580.48633	PPL: 1.30045	bleu: 0.00000	LR: 0.00062500	
Steps: 940	Loss: 3580.79810	PPL: 1.30048	bleu: 0.00000	LR: 0.00062500	
Steps: 950	Loss: 3580.71533	PPL: 1.30047	bleu: 0.00000	LR: 0.00062500	
Steps: 960	Loss: 3579.79126	PPL: 1.30038	bleu: 0.00000	LR: 0.00031250	
Steps: 970	Loss: 3580.28101	PPL: 1.30043	bleu: 0.00000	LR: 0.00031250	
Steps: 980	Loss: 3580.50073	PPL: 1.30045	bleu: 0.00000	LR: 0.00031250	
Steps: 990	Loss: 3579.73975	PPL: 1.30038	bleu: 0.00000	LR: 0.00031250	*
Steps: 1000	Loss: 3579.98120	PPL: 1.30040	bleu: 0.00000	LR: 0.00031250	
Steps: 1010	Loss: 3580.55859	PPL: 1.30046	bleu: 0.00000	LR: 0.00031250	
Steps: 1020	Loss: 3582.33203	PPL: 1.30063	bleu: 0.00000	LR: 0.00031250	
Steps: 1030	Loss: 3581.53589	PPL: 1.30055	bleu: 0.00000	LR: 0.00031250	
Steps: 1040	Loss: 3579.61597	PPL: 1.30037	bleu: 0.00000	LR: 0.00031250	*
Steps: 1050	Loss: 3579.63818	PPL: 1.30037	bleu: 0.00000	LR: 0.00031250	
Steps: 1060	Loss: 3580.41138	PPL: 1.30044	bleu: 0.00000	LR: 0.00031250	
Steps: 1070	Loss: 3582.11206	PPL: 1.30061	bleu: 0.00000	LR: 0.00031250	
Steps: 1080	Loss: 3582.06348	PPL: 1.30060	bleu: 0.00000	LR: 0.00031250	
Steps: 1090	Loss: 3581.48877	PPL: 1.30055	bleu: 0.00000	LR: 0.00031250	
Steps: 1100	Loss: 3581.87061	PPL: 1.30058	bleu: 0.00000	LR: 0.00015625	
Steps: 1110	Loss: 3581.00659	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1120	Loss: 3580.96680	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1130	Loss: 3581.01660	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1140	Loss: 3580.28760	PPL: 1.30043	bleu: 0.00000	LR: 0.00015625	
Steps: 1150	Loss: 3580.99316	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1160	Loss: 3581.49414	PPL: 1.30055	bleu: 0.00000	LR: 0.00007813	
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$ cat ./translate.log 
2022-02-26 17:06:02,582 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:06:02,611 - DEBUG - joeynmt.prediction - Process device: cpu, n_gpu: 0
2022-02-26 17:06:02,611 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 17:06:02,615 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:06:02,618 - INFO - joeynmt.model - Enc-dec model built.
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$
```

log ဖိုင်တွေကို ကြည့်တော့ BLEU score တွေက zero အဆင့်မှာပဲ ရှိသေးတော့ configuration ဖိုင်ကို ပြန်ကြည့်ပြီး update လုပ်သင့်တာ လုပ်ရလိမ့်မယ်လို့ ထင်တယ်...  

## Learn Small Config File and Updating

ပထမ run တုန်းက vocab ဖိုင်ကို marian တုန်းက ဆောက်ခဲ့တဲ့ vocab ဖိုင်ကို assign လုပ်ခဲ့တာ...  

```
src_vocab: "/media/ye/project2/exp/myrk-transformer/data/syl/vocab/vocab.my.yml"
    # trg_vocab: "my_model/trg_vocab.txt"  # one token per line, line number is index            
    trg_vocab: "/media/ye/project2/exp/myrk-transformer/data/syl/vocab/vocab.rk.yml"
```

အဲဒါကို ပိတ်ကြည့်မယ် ...  

ပထမ run တုန်းက epochs: 1, Validation_freq: 10 ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်...  

```
epochs: 30                       # train for this many epochs
validation_freq: 1000             # validate after this many updates (number of mini-batches), default: 1000
```
    
loging freq ကိုလည်း ၁၀ ကနေ ၁၀၀ အဖြစ် ပြောင်းခဲ့တယ်...   

```
logging_freq: 100                # log the training progress after this many updates, default: 100
```

ပြီးတော့... GPU ပါ သုံးကြည့်မယ်  

```
    use_cuda: True                 # use CUDA for acceleration on GPU, required. Set to False when working on CPU.
```

## ReTraining RNN with JoeyNMt for RK-MY (Syllable)

အထက်ပါအတိုင်း config ဖိုင်ကို update လုပ်ပြီးနောက် ထပ် training လုပ်ကြည့်ခဲ့...  

```
(joey) ye@:~/exp/joeynmt/configs$ vi ./transformer_copy.yaml 
(joey) ye@:~/exp/joeynmt/configs$ 
(joey) ye@:~/exp/joeynmt/configs$ cd ..
(joey) ye@:~/exp/joeynmt$ 
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/small.myrk.yaml 
2022-02-26 17:20:11,561 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:20:11,578 - INFO - joeynmt.data - Loading training data...
2022-02-26 17:20:11,778 - INFO - joeynmt.data - Building vocabulary...
2022-02-26 17:20:11,855 - INFO - joeynmt.data - Loading dev data...
2022-02-26 17:20:11,866 - INFO - joeynmt.data - Loading test data...
2022-02-26 17:20:11,885 - INFO - joeynmt.data - Data loaded.
2022-02-26 17:20:11,885 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:20:11,888 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 17:20:11.966605: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-26 17:20:12,675 - INFO - joeynmt.training - Total params: 161104
2022-02-26 17:20:12,676 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                           cfg.name : my_experiment
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.data.random_train_subset : -1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 30
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -            cfg.testing.postprocess : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -               cfg.testing.bpe_type : subword-nmt
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers - cfg.testing.sacrebleu.remove_whitespace : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -     cfg.testing.sacrebleu.tokenize : 13a
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -            cfg.training.adam_betas : [0.9, 0.999]
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.005
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0001
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -         cfg.training.clip_grad_val : 1.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.eval_batch_size : 10
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.eval_batch_type : sentence
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -      cfg.training.batch_multiplier : 1
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -         cfg.training.normalization : batch
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -                cfg.training.epochs : 30
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : loss
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/small_model_myrk
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -              cfg.training.use_cuda : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -                  cfg.training.fp16 : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 31
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 3
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.label_smoothing : 0.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.use_reinforcement_learning : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.method : reinforce
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.log_probabilities : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.pickle_logs : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.topk : 20
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.temperature : 1
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.reward : bleu
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.baseline : average_reward_baseline
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.alpha : 0.005
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.samples : 5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.add_gold : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.critic_learning_rate : 5e-06
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -              cfg.model.init_weight : 0.01
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -                cfg.model.init_gain : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.embed_init_gain : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.tied_embeddings : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.tied_softmax : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.encoder.type : recurrent
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : gru
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 30
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 3
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -           cfg.model.encoder.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.decoder.type : recurrent
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : gru
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 30
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : last
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -           cfg.model.decoder.freeze : False
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Data set sizes: 
	train 15324,
	valid 1000,
	test 1811
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) ကို (7) အ (8) တယ် (9) သူ
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) မ (8) ရေ (9) ပါ
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Number of Src words (types): 1552
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Number of Trg words (types): 1662
2022-02-26 17:20:12,679 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(GRU(16, 30, num_layers=3, batch_first=True, dropout=0.2, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=GRU(46, 30, num_layers=2, batch_first=True, dropout=0.2), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=1552),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=1662))
2022-02-26 17:20:12,680 - INFO - joeynmt.training - Train stats:
	device: cpu
	n_gpu: 0
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 10
	total batch size (w. parallel & accumulation): 10
2022-02-26 17:20:12,680 - INFO - joeynmt.training - EPOCH 1
2022-02-26 17:20:20,858 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    72.434441, Tokens per Sec:     1626, Lr: 0.005000
...
...
...
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 17:59:32,673 - INFO - joeynmt.training - Epoch  16, Step:    24100, Batch Loss:    33.629875, Tokens per Sec:     1509, Lr: 0.005000
2022-02-26 17:59:40,632 - INFO - joeynmt.training - Epoch  16, Step:    24200, Batch Loss:    44.099648, Tokens per Sec:     1659, Lr: 0.005000
2022-02-26 17:59:49,927 - INFO - joeynmt.training - Epoch  16, Step:    24300, Batch Loss:    25.616074, Tokens per Sec:     1410, Lr: 0.005000
2022-02-26 17:59:59,881 - INFO - joeynmt.training - Epoch  16, Step:    24400, Batch Loss:    35.911987, Tokens per Sec:     1321, Lr: 0.005000
2022-02-26 18:00:09,425 - INFO - joeynmt.training - Epoch  16, Step:    24500, Batch Loss:    40.154503, Tokens per Sec:     1395, Lr: 0.005000
2022-02-26 18:00:12,227 - INFO - joeynmt.training - Epoch  16: total training loss 53995.52
2022-02-26 18:00:12,228 - INFO - joeynmt.training - EPOCH 17
2022-02-26 18:00:19,006 - INFO - joeynmt.training - Epoch  17, Step:    24600, Batch Loss:    45.319824, Tokens per Sec:     1426, Lr: 0.005000
2022-02-26 18:00:28,422 - INFO - joeynmt.training - Epoch  17, Step:    24700, Batch Loss:    48.196053, Tokens per Sec:     1407, Lr: 0.005000
2022-02-26 18:00:37,692 - INFO - joeynmt.training - Epoch  17, Step:    24800, Batch Loss:    41.469799, Tokens per Sec:     1393, Lr: 0.005000
2022-02-26 18:00:46,628 - INFO - joeynmt.training - Epoch  17, Step:    24900, Batch Loss:    33.750587, Tokens per Sec:     1473, Lr: 0.005000
2022-02-26 18:00:56,075 - INFO - joeynmt.training - Epoch  17, Step:    25000, Batch Loss:    33.245201, Tokens per Sec:     1367, Lr: 0.005000
...
...
...
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 18:35:02,499 - INFO - joeynmt.training - Epoch  30, Step:    45100, Batch Loss:    41.235615, Tokens per Sec:     1050, Lr: 0.005000
2022-02-26 18:35:14,238 - INFO - joeynmt.training - Epoch  30, Step:    45200, Batch Loss:    34.890701, Tokens per Sec:     1115, Lr: 0.005000
2022-02-26 18:35:26,784 - INFO - joeynmt.training - Epoch  30, Step:    45300, Batch Loss:    28.857077, Tokens per Sec:     1052, Lr: 0.005000
2022-02-26 18:35:40,156 - INFO - joeynmt.training - Epoch  30, Step:    45400, Batch Loss:    25.483398, Tokens per Sec:      995, Lr: 0.005000
2022-02-26 18:35:50,827 - INFO - joeynmt.training - Epoch  30, Step:    45500, Batch Loss:    32.120075, Tokens per Sec:     1242, Lr: 0.005000
2022-02-26 18:35:59,826 - INFO - joeynmt.training - Epoch  30, Step:    45600, Batch Loss:    28.888306, Tokens per Sec:     1471, Lr: 0.005000
2022-02-26 18:36:09,389 - INFO - joeynmt.training - Epoch  30, Step:    45700, Batch Loss:    32.717991, Tokens per Sec:     1363, Lr: 0.005000
2022-02-26 18:36:20,539 - INFO - joeynmt.training - Epoch  30, Step:    45800, Batch Loss:    35.522102, Tokens per Sec:     1172, Lr: 0.005000
2022-02-26 18:36:34,107 - INFO - joeynmt.training - Epoch  30, Step:    45900, Batch Loss:    23.591614, Tokens per Sec:      975, Lr: 0.005000
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Epoch  30: total training loss 49794.87
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Best validation result (greedy) at step    43000: 33397.05 loss.
2022-02-26 18:36:42,338 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 18:36:42,338 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/43000.ckpt
2022-02-26 18:36:42,341 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 18:36:42,344 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 18:36:42,344 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction -  dev bleu[13a]:  20.05 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00043000.hyps.dev
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 18:36:59,325 - INFO - joeynmt.prediction - test bleu[13a]:  19.75 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 18:36:59,326 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00043000.hyps.test

real	76m49.270s
user	543m19.766s
sys	2m3.014s
(joey) ye@:~/exp/joeynmt$ 
```

## Testing with RNN Model My-RK (Syllable)

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt translate configs/small.myrk.yaml < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./models/small_model_myrk/myrk.syl.out2
2022-02-26 18:39:11,691 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 18:39:11,722 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 18:39:11,725 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 18:39:11,729 - INFO - joeynmt.model - Enc-dec model built.

real	0m11.509s
user	1m16.510s
sys	0m0.846s
(joey) ye@:~/exp/joeynmt$ head ./models/small_model_myrk/myrk.syl.out2
သူ အ မှန် အ ခါး မ တိ ပီး ပါ လား ။
ကျွန် တော် အ ယောက် လို ပီး ဖို့ ။
ပြ ပြီး ရေ အ တွက် ကို သ င့် ရေ ။
မင်း အ တွက် စိတ် မ ပြော ပါ ။
ထို မ ချေ ကို ထို မ ချေ ဂ ရု မ ဟုတ် ခ ပါ ။
ကိုယ် မင်း ကို လုပ် ခ ပါ ရေ ။
ငါ အ လုပ် မ လုပ် ပါ ။
ကျွန် တော် ဘတ်စ် ရာ ဟိ ရေ အ တွက် အ ထင် ကျွန် တော် ထင် ပါ ။
ည အ ခါး က အ ချိန် မ သူ ရို့ ဇာ စား နီ စွာ လေး ။
မင်း ကိုယ် တိ ကို တွိ နီ ပါ လား ။
(joey) ye@:~/exp/joeynmt$ head /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရီ ကို သောက် သ င့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
(joey) ye@:~/exp/joeynmt$ 

```

Validation ရလဒ်တွေကို ကြည့်တော့ ပထမဆုံး run တာထက်တော့ တိုးတက်လာတာကို တွေ့ရ...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/small_model_myrk/validations.txt 
Steps: 1000	Loss: 57388.25000	PPL: 67.40676	bleu: 0.52890	LR: 0.00500000	*
Steps: 2000	Loss: 53066.17188	PPL: 49.08836	bleu: 2.10495	LR: 0.00500000	*
Steps: 3000	Loss: 51286.50000	PPL: 43.07927	bleu: 1.86128	LR: 0.00500000	*
Steps: 4000	Loss: 49999.86719	PPL: 39.19848	bleu: 3.05241	LR: 0.00500000	*
Steps: 5000	Loss: 48785.27344	PPL: 35.85632	bleu: 3.38970	LR: 0.00500000	*
Steps: 6000	Loss: 48083.76953	PPL: 34.05743	bleu: 3.76580	LR: 0.00500000	*
Steps: 7000	Loss: 47666.36328	PPL: 33.03019	bleu: 4.05210	LR: 0.00500000	*
Steps: 8000	Loss: 46393.51562	PPL: 30.08508	bleu: 4.76296	LR: 0.00500000	*
Steps: 9000	Loss: 45679.07812	PPL: 28.54863	bleu: 5.94355	LR: 0.00500000	*
Steps: 10000	Loss: 44743.05078	PPL: 26.65375	bleu: 6.83491	LR: 0.00500000	*
Steps: 11000	Loss: 43662.57422	PPL: 24.62229	bleu: 7.07079	LR: 0.00500000	*
Steps: 12000	Loss: 43629.57031	PPL: 24.56274	bleu: 7.94861	LR: 0.00500000	*
Steps: 13000	Loss: 43006.12500	PPL: 23.46445	bleu: 8.60597	LR: 0.00500000	*
Steps: 14000	Loss: 42187.97266	PPL: 22.09731	bleu: 9.23368	LR: 0.00500000	*
Steps: 15000	Loss: 40580.71094	PPL: 19.63918	bleu: 9.68358	LR: 0.00500000	*
Steps: 16000	Loss: 39141.94531	PPL: 17.67162	bleu: 10.84861	LR: 0.00500000	*
Steps: 17000	Loss: 38644.76172	PPL: 17.03859	bleu: 11.43360	LR: 0.00500000	*
Steps: 18000	Loss: 38167.29297	PPL: 16.45200	bleu: 12.91926	LR: 0.00500000	*
Steps: 19000	Loss: 37345.45703	PPL: 15.48926	bleu: 13.24043	LR: 0.00500000	*
Steps: 20000	Loss: 37135.27344	PPL: 15.25222	bleu: 12.98069	LR: 0.00500000	*
Steps: 21000	Loss: 36692.06641	PPL: 14.76420	bleu: 13.46621	LR: 0.00500000	*
Steps: 22000	Loss: 36376.33984	PPL: 14.42611	bleu: 13.95958	LR: 0.00500000	*
Steps: 23000	Loss: 36217.14062	PPL: 14.25858	bleu: 13.78189	LR: 0.00500000	*
Steps: 24000	Loss: 36333.26172	PPL: 14.38058	bleu: 14.53253	LR: 0.00500000	
Steps: 25000	Loss: 35629.09766	PPL: 13.65646	bleu: 14.67296	LR: 0.00500000	*
Steps: 26000	Loss: 35683.49609	PPL: 13.71107	bleu: 14.58215	LR: 0.00500000	
Steps: 27000	Loss: 35626.93750	PPL: 13.65429	bleu: 14.22184	LR: 0.00500000	*
Steps: 28000	Loss: 35178.08594	PPL: 13.21193	bleu: 15.12416	LR: 0.00500000	*
Steps: 29000	Loss: 35752.49219	PPL: 13.78066	bleu: 15.34604	LR: 0.00500000	
Steps: 30000	Loss: 35008.98828	PPL: 13.04902	bleu: 15.54186	LR: 0.00500000	*
Steps: 31000	Loss: 34669.69141	PPL: 12.72817	bleu: 15.22020	LR: 0.00500000	*
Steps: 32000	Loss: 34336.41797	PPL: 12.42070	bleu: 15.56523	LR: 0.00500000	*
Steps: 33000	Loss: 34719.87109	PPL: 12.77512	bleu: 16.37965	LR: 0.00500000	
Steps: 34000	Loss: 35017.46875	PPL: 13.05714	bleu: 15.91264	LR: 0.00500000	
Steps: 35000	Loss: 34258.24219	PPL: 12.34966	bleu: 16.28863	LR: 0.00500000	*
Steps: 36000	Loss: 34083.28516	PPL: 12.19214	bleu: 17.78684	LR: 0.00500000	*
Steps: 37000	Loss: 33634.72656	PPL: 11.79740	bleu: 17.82240	LR: 0.00500000	*
Steps: 38000	Loss: 33990.19922	PPL: 12.10915	bleu: 17.05839	LR: 0.00500000	
Steps: 39000	Loss: 34116.59766	PPL: 12.22198	bleu: 17.18198	LR: 0.00500000	
Steps: 40000	Loss: 34182.85156	PPL: 12.28154	bleu: 17.61039	LR: 0.00500000	
Steps: 41000	Loss: 38095.79688	PPL: 16.36592	bleu: 16.39524	LR: 0.00500000	
Steps: 42000	Loss: 33579.71094	PPL: 11.74988	bleu: 17.89235	LR: 0.00500000	*
Steps: 43000	Loss: 33397.05078	PPL: 11.59345	bleu: 18.63332	LR: 0.00500000	*
Steps: 44000	Loss: 34700.21875	PPL: 12.75671	bleu: 17.97865	LR: 0.00500000	
Steps: 45000	Loss: 33715.35156	PPL: 11.86740	bleu: 17.83172	LR: 0.00500000	
(joey) ye@:~/exp/joeynmt$ 
```

## Training My-RK with wmt_myrk_default.yaml

ဒီတစ်ခါ config ဖိုင်ကို တကယ့် WMT မှာ default အဖြစ် သုံးခဲ့တဲ့ ဖိုင်ကို မြန်မာ-ရခိုင်အတွက် ဝင်ပြင်ပြီး မော်ဒယ်ဆောက်ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt/configs$ cat ./wmt_myrk_default.yaml 
name: "wmt_ende_default"

data:
    src: "my"
    trg: "rk"
    train: "/media/ye/project2/exp/myrk-transformer/data/syl/train"    # training data
    dev: "/media/ye/project2/exp/myrk-transformer/data/syl/dev"        # development data for validation
    test: "/media/ye/project2/exp/myrk-transformer/data/syl/test"      # test data for testing final model; optional    
    level: "word"
    lowercase: False
    max_sent_length: 50
    src_voc_min_freq: 0
    src_voc_limit: 100000
    trg_voc_min_freq: 0
    trg_voc_limit: 100000

testing:
    beam_size: 5
    alpha: 1.0

training:
    random_seed: 42
    optimizer: "adam"
    learning_rate: 0.0003
    learning_rate_min: 0.0000005
    weight_decay: 0.0
    clip_grad_norm: 1.0
    batch_size: 80
    scheduling: "plateau"
    patience: 10
    decrease_factor: 0.5
    early_stopping_metric: "eval_metric"
    epochs: 20
    validation_freq: 7362
    logging_freq: 1000
    eval_metric: "bleu"
    model_dir: "models/wmt_myrk_default"
    overwrite: False
    shuffle: True
    use_cuda: True
    max_output_length: 100
    print_valid_sents: [0, 1, 2]

model:
    encoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 500
            scale: False
        hidden_size: 500
        bidirectional: True
        dropout: 0.2
        num_layers: 1
    decoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 500
            scale: False
        emb_scale: False
        hidden_size: 1000
        dropout: 0.2
        hidden_dropout: 0.2
        num_layers: 1
        input_feeding: True
        init_hidden: "bridge"
        attention: "bahdanau"
(joey) ye@:~/exp/joeynmt/configs$ 
```

run ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
2022-02-26 19:02:34,633 - INFO - joeynmt.training - Epoch   6, Step:     1000, Batch Loss:    15.628224, Tokens per Sec:     1821, Lr: 0.000300
2022-02-26 19:04:16,461 - INFO - joeynmt.training - Epoch   6: total training loss 2426.79
2022-02-26 19:04:16,461 - INFO - joeynmt.training - EPOCH 7
2022-02-26 19:06:12,215 - INFO - joeynmt.training - Epoch   7: total training loss 1954.65
2022-02-26 19:06:12,215 - INFO - joeynmt.training - EPOCH 8
2022-02-26 19:08:09,133 - INFO - joeynmt.training - Epoch   8: total training loss 1500.09
2022-02-26 19:08:09,133 - INFO - joeynmt.training - EPOCH 9
2022-02-26 19:10:06,317 - INFO - joeynmt.training - Epoch   9: total training loss 1092.61
2022-02-26 19:10:06,317 - INFO - joeynmt.training - EPOCH 10
2022-02-26 19:12:03,155 - INFO - joeynmt.training - Epoch  10: total training loss 788.03
2022-02-26 19:12:03,155 - INFO - joeynmt.training - EPOCH 11
2022-02-26 19:12:33,894 - INFO - joeynmt.training - Epoch  11, Step:     2000, Batch Loss:     2.603220, Tokens per Sec:     1774, Lr: 0.000300
2022-02-26 19:14:00,143 - INFO - joeynmt.training - Epoch  11: total training loss 618.69
2022-02-26 19:14:00,143 - INFO - joeynmt.training - EPOCH 12
2022-02-26 19:15:57,283 - INFO - joeynmt.training - Epoch  12: total training loss 514.09
2022-02-26 19:15:57,284 - INFO - joeynmt.training - EPOCH 13
2022-02-26 19:17:53,280 - INFO - joeynmt.training - Epoch  13: total training loss 439.72
2022-02-26 19:17:53,280 - INFO - joeynmt.training - EPOCH 14
2022-02-26 19:19:49,555 - INFO - joeynmt.training - Epoch  14: total training loss 381.92
2022-02-26 19:19:49,555 - INFO - joeynmt.training - EPOCH 15
2022-02-26 19:21:45,768 - INFO - joeynmt.training - Epoch  15: total training loss 338.48
2022-02-26 19:21:45,768 - INFO - joeynmt.training - EPOCH 16
2022-02-26 19:22:30,393 - INFO - joeynmt.training - Epoch  16, Step:     3000, Batch Loss:     2.129778, Tokens per Sec:     1824, Lr: 0.000300
2022-02-26 19:23:41,149 - INFO - joeynmt.training - Epoch  16: total training loss 301.70
2022-02-26 19:23:41,149 - INFO - joeynmt.training - EPOCH 17
2022-02-26 19:25:37,394 - INFO - joeynmt.training - Epoch  17: total training loss 268.87
2022-02-26 19:25:37,394 - INFO - joeynmt.training - EPOCH 18
2022-02-26 19:27:34,094 - INFO - joeynmt.training - Epoch  18: total training loss 234.00
2022-02-26 19:27:34,094 - INFO - joeynmt.training - EPOCH 19
2022-02-26 19:29:29,690 - INFO - joeynmt.training - Epoch  19: total training loss 204.30
2022-02-26 19:29:29,690 - INFO - joeynmt.training - EPOCH 20
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Epoch  20: total training loss 180.29
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-26 19:31:24,897 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-26 19:31:24,898 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint models/wmt_myrk_default/0.ckpt not found

real	38m57.669s
user	43m24.300s
sys	8m51.045s
(joey) ye@:~/exp/joeynmt$
```

အဲဒါနဲ့ model_dir ရဲ့ path ကို full path ပေးပြီး ပြန် train ခဲ့...  

```
    model_dir: "/home/ye/exp/joeynmt/models/wmt_myrk_default"
```

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 806, in train
    model_dir = make_model_dir(cfg["training"]["model_dir"],
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 44, in make_model_dir
    raise FileExistsError(
FileExistsError: Model directory exists and overwriting is disabled.

real	0m1.694s
user	0m1.063s
sys	0m0.707s
(joey) ye@:~/exp/joeynmt$
```

overwrite ကို True ထားပြီး train မှ ရလိမ့်မယ်...  

```
    overwrite: True
```

train လုပ်ကြည့်တော့ စောစောကလိုပဲ error တက်နေသေးတယ်...?!  

```
2022-02-26 20:34:09,992 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-26 20:34:10,002 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-26 20:34:10,002 - INFO - joeynmt.prediction - Loading model from /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt not found

real	39m6.048s
user	43m45.978s
sys	8m33.931s
(joey) ye@:~/exp/joeynmt$
```

config ဖိုင်ရဲ့ ထိပ်ဆုံး နာမည်ကို original configuration အတိုင်း ထားမိတဲ့ error ကိုတော့ တွေ့ပြီ... အဲဒါကြောင့်လား?!  

```
name: "wmt_ende_default" ကို 
name: "wmt_myrk_default"
```

Error အတူတူပဲ ပေးနေတယ်...  


```
    lowercase: True
```

lowercase ကို True လုပ်ပြီး ထပ် training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 00:13:02,865 - INFO - joeynmt.training - EPOCH 20
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Epoch  20: total training loss 180.29
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 00:14:59,154 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 00:14:59,154 - INFO - joeynmt.prediction - Loading model from /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt not found

real	39m11.235s
user	43m42.326s
sys	8m45.116s
(joey) ye@:~/exp/joeynmt$ 

```

ဒီ error ပဲ ထပ်ပေးနေတယ်...  

```
    logging_freq: 100
    keep_last_ckpts: 3              # keep this many of the latest checkpoints, if -1: all of them, default: 5
```

small_model_myrk/ ဖိုလ်ဒါအောက်ကို ကြည့်ကြည့်တော့...  
best.ckpt၊ latest.ckpt  နှစ်ဖိုင်ကိုတော့ တွေ့ရတယ်။ training လုပ်နေတဲ့အချိန်မှာတော့ မပြောတတ်ဘူး...  

ထပ် training လုပ်ကြည့်ခဲ့...  
Same ERROR!!!  

code ကို ဝင်ကြည့်တော့ ...  
(File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint)  

```python
    # when checkpoint is not specified, take latest (best) from model dir
    if ckpt is None:
        ckpt = get_latest_checkpoint(model_dir)
        try:
            step = ckpt.split(model_dir+"/")[1].split(".ckpt")[0]
        except IndexError:
            step = "best"
```

path ကို အပြည့်မပေးပဲ run ကြည့်ခဲ့...  

```
#    model_dir: "/home/ye/exp/joeynmt/models/wmt_myrk_default"
    model_dir: "wmt_myrk_default"
```

same error ပဲ ပေးနေ...  
အောက်ပါ configuration parameter သုံးခုကို ပေးခဲ့...  

```
training:
    #load_model: "models/small_model/60.ckpt" # if given, load a pre-trained model from this checkpoint
    reset_best_ckpt: False          # if True, reset the tracking of the best checkpoint and scores. Use for domain adaptation or fine-tuning with new metrics or dev data.
    reset_scheduler: False          # if True, overwrite scheduler in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.
    reset_optimizer: False          # if True, overwrite optimizer in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.
```

debug လုပ်ရတာ မြန်အောင်လို့ epochs: 10 ထားပြီးတော့ ထပ် training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Epoch  10: total training loss 788.03
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 08:47:15,862 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 08:47:15,862 - INFO - joeynmt.prediction - Loading model from wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint wmt_myrk_default/0.ckpt not found

real	19m4.202s
user	21m15.634s
sys	4m19.876s
(joey) ye@:~/exp/joeynmt$
```

ဒီတစ်ခါတော့ keep_last_ckpts ဆိုတဲ့ option ကို default value အဖြစ် setting ချိန်ထားခဲ့...  

```
    keep_last_ckpts: 5              # keep this many of the latest checkpoints, if -1: all of them, default: 5
```

model folder ကိုလည်း ဖျက်ခဲ့ပြီး...  

```
(joey) ye@:~/exp/joeynmt/models$ rm -rf wmt_myrk_default/ 
```
ထပ် run ကြည့်ခဲ့...  

```
2022-02-27 09:15:38,744 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 09:15:38,744 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 09:15:38,754 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 09:15:38,755 - INFO - joeynmt.prediction - Loading model from wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint wmt_myrk_default/0.ckpt not found

real	19m4.514s
user	21m17.273s
sys	4m17.999s
(joey) ye@:~/exp/joeynmt$ 
```

WTF! ...  
မော်ဒယ်ကို မဆောက်ပေးနိုင်တာ လို့ ထင်တယ်။ memory မနိုင်တဲ့ error ဘာညာလည်း မပေးပေမဲ့ hidden_size ကို လျှော့ကြည့်ခဲ့...  

```
model:
    encoder:
        hidden_size: 500 ကို
        hidden_size: 30
        
    decoder:
        hidden_size: 30

```

ထပ် run ကြည့်ခဲ့...  
Got ERROR!!!

```
    validation_freq: 7362 ကို
    validation_freq: 1000 ပြောင်း
    
        embeddings:
            embedding_dim: 16    
```
အထက်ပါအတိုင်း parameter တချို့ကို ပြင်ဆင်ပြီးတော့... ထပ် run ကြည့်ခဲ့

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
2022-02-27 10:28:50,418 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 10:28:50,435 - INFO - joeynmt.data - Loading training data...
2022-02-27 10:28:50,630 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 10:28:50,706 - INFO - joeynmt.data - Loading dev data...
2022-02-27 10:28:50,717 - INFO - joeynmt.data - Loading test data...
2022-02-27 10:28:50,736 - INFO - joeynmt.data - Data loaded.
2022-02-27 10:28:50,736 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:28:50,746 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:28:50.824941: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-27 10:28:51,467 - INFO - joeynmt.training - Total params: 1011932
2022-02-27 10:28:51,469 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                           cfg.name : wmt_myrk_default
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 50
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100000
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100000
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0003
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 5e-07
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -            cfg.training.batch_size : 80
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -              cfg.training.patience : 10
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -                cfg.training.epochs : 10
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt_myrk_default
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 500
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 30
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -        cfg.model.decoder.emb_scale : False
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 30
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : bridge
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Data set sizes: 
	train 15535,
	valid 1000,
	test 1811
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Number of Src words (types): 1580
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Number of Trg words (types): 1687
2022-02-27 10:28:53,021 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(500, 30, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(46, 30, batch_first=True), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=500, vocab_size=1580),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=1687))
2022-02-27 10:28:53,022 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 40
	total batch size (w. parallel & accumulation): 80
2022-02-27 10:28:53,022 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 10:29:00,311 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    41.147419, Tokens per Sec:    14867, Lr: 0.000300
2022-02-27 10:29:05,484 - INFO - joeynmt.training - Epoch   1: total training loss 8464.12
2022-02-27 10:29:05,484 - INFO - joeynmt.training - EPOCH 2
2022-02-27 10:29:05,765 - INFO - joeynmt.training - Epoch   2, Step:      200, Batch Loss:    34.781780, Tokens per Sec:    19317, Lr: 0.000300
2022-02-27 10:29:11,507 - INFO - joeynmt.training - Epoch   2, Step:      300, Batch Loss:    34.522808, Tokens per Sec:    18908, Lr: 0.000300
2022-02-27 10:29:16,658 - INFO - joeynmt.training - Epoch   2: total training loss 6916.50
2022-02-27 10:29:16,658 - INFO - joeynmt.training - EPOCH 3
2022-02-27 10:29:17,303 - INFO - joeynmt.training - Epoch   3, Step:      400, Batch Loss:    34.547497, Tokens per Sec:    16497, Lr: 0.000300
2022-02-27 10:29:23,244 - INFO - joeynmt.training - Epoch   3, Step:      500, Batch Loss:    34.913837, Tokens per Sec:    18193, Lr: 0.000300
2022-02-27 10:29:28,105 - INFO - joeynmt.training - Epoch   3: total training loss 6710.48
2022-02-27 10:29:28,105 - INFO - joeynmt.training - EPOCH 4
2022-02-27 10:29:28,942 - INFO - joeynmt.training - Epoch   4, Step:      600, Batch Loss:    30.318647, Tokens per Sec:    18848, Lr: 0.000300
2022-02-27 10:29:34,446 - INFO - joeynmt.training - Epoch   4, Step:      700, Batch Loss:    34.668171, Tokens per Sec:    19680, Lr: 0.000300
2022-02-27 10:29:38,987 - INFO - joeynmt.training - Epoch   4: total training loss 6642.92
2022-02-27 10:29:38,987 - INFO - joeynmt.training - EPOCH 5
2022-02-27 10:29:40,095 - INFO - joeynmt.training - Epoch   5, Step:      800, Batch Loss:    35.233486, Tokens per Sec:    19366, Lr: 0.000300
2022-02-27 10:29:45,682 - INFO - joeynmt.training - Epoch   5, Step:      900, Batch Loss:    30.308668, Tokens per Sec:    19306, Lr: 0.000300
2022-02-27 10:29:49,885 - INFO - joeynmt.training - Epoch   5: total training loss 6459.74
2022-02-27 10:29:49,885 - INFO - joeynmt.training - EPOCH 6
2022-02-27 10:29:51,243 - INFO - joeynmt.training - Epoch   6, Step:     1000, Batch Loss:    35.419918, Tokens per Sec:    19812, Lr: 0.000300
2022-02-27 10:29:52,436 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-27 10:29:52,453 - INFO - joeynmt.training - Example #0
2022-02-27 10:29:52,453 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-27 10:29:52,453 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Example #1
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။ ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Example #2
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Validation result (greedy) at epoch   6, step     1000: bleu:   0.01, loss: 33062.2891, ppl:  11.3122, duration: 1.2105s
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 10:29:58,533 - INFO - joeynmt.training - Epoch   6, Step:     1100, Batch Loss:    34.886578, Tokens per Sec:    17815, Lr: 0.000300
2022-02-27 10:30:02,465 - INFO - joeynmt.training - Epoch   6: total training loss 6313.00
2022-02-27 10:30:02,466 - INFO - joeynmt.training - EPOCH 7
2022-02-27 10:30:04,122 - INFO - joeynmt.training - Epoch   7, Step:     1200, Batch Loss:    33.299118, Tokens per Sec:    19435, Lr: 0.000300
2022-02-27 10:30:09,780 - INFO - joeynmt.training - Epoch   7, Step:     1300, Batch Loss:    33.795162, Tokens per Sec:    19147, Lr: 0.000300
2022-02-27 10:30:13,262 - INFO - joeynmt.training - Epoch   7: total training loss 6190.45
2022-02-27 10:30:13,262 - INFO - joeynmt.training - EPOCH 8
2022-02-27 10:30:15,168 - INFO - joeynmt.training - Epoch   8, Step:     1400, Batch Loss:    32.178890, Tokens per Sec:    19892, Lr: 0.000300
2022-02-27 10:30:20,875 - INFO - joeynmt.training - Epoch   8, Step:     1500, Batch Loss:    31.339453, Tokens per Sec:    18946, Lr: 0.000300
2022-02-27 10:30:24,163 - INFO - joeynmt.training - Epoch   8: total training loss 6072.78
2022-02-27 10:30:24,163 - INFO - joeynmt.training - EPOCH 9
2022-02-27 10:30:26,403 - INFO - joeynmt.training - Epoch   9, Step:     1600, Batch Loss:    33.533947, Tokens per Sec:    19340, Lr: 0.000300
2022-02-27 10:30:32,029 - INFO - joeynmt.training - Epoch   9, Step:     1700, Batch Loss:    31.088232, Tokens per Sec:    19315, Lr: 0.000300
2022-02-27 10:30:35,060 - INFO - joeynmt.training - Epoch   9: total training loss 5961.14
2022-02-27 10:30:35,060 - INFO - joeynmt.training - EPOCH 10
2022-02-27 10:30:37,640 - INFO - joeynmt.training - Epoch  10, Step:     1800, Batch Loss:    32.837299, Tokens per Sec:    18733, Lr: 0.000300
2022-02-27 10:30:43,311 - INFO - joeynmt.training - Epoch  10, Step:     1900, Batch Loss:    30.626780, Tokens per Sec:    19128, Lr: 0.000300
2022-02-27 10:30:46,033 - INFO - joeynmt.training - Epoch  10: total training loss 5867.65
2022-02-27 10:30:46,034 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 10:30:46,034 - INFO - joeynmt.training - Best validation result (greedy) at step     1000:   0.01 eval_metric.
2022-02-27 10:30:46,042 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 10:30:46,042 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/1000.ckpt
2022-02-27 10:30:46,051 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:30:46,061 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:30:46,065 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00001000.hyps.dev
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 10:30:54,915 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:30:54,916 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00001000.hyps.test

real	2m6.122s
user	3m14.651s
sys	0m10.797s
(joey) ye@:~/exp/joeynmt$ 


```

ဒီတစ်ခါတော့ အဆင်ပြေပြေနဲ့ training လုပ်လို့ ရသွားပြီ။ ပြဿနာက "embedding_dim: 16" ကြောင့် ဖြစ်နေတာလို့ ယူဆတယ်...  

model ဖိုလ်ဒါထဲ ဝင်ကြည့်ခဲ့...  
ပုံမှန် အခြေအနေလိုတော့ မြင်ရ  

```
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ ls
00001000.hyps.dev   1000.ckpt  att.1000.0.pdf  att.1000.2.pdf  config.yaml  src_vocab.txt  train.log      validations.txt
00001000.hyps.test  1000.hyps  att.1000.1.pdf  best.ckpt       latest.ckpt  tensorboard    trg_vocab.txt
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ cat validations.txt 
Steps: 1000	Loss: 33062.28906	PPL: 11.31215	bleu: 0.01426	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ 
```

epoch ကို တိုးကြည့်မယ်။ embedding_dim ကိုလည်း တိုးကြည့်မယ်  

```
    epochs: 30
     embedding_dim: 64 # for encoder
      embedding_dim: 64 # for decoder
```

ထပ် run ကြည့်ခဲ့... validation မှာလည်း BLEU က ကောင်းမှ testing မှာလည်း ကောင်းမှာမို့...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
...
...
2022-02-27 10:45:47,871 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:    23.637800, Tokens per Sec:    19045, Lr: 0.000300
2022-02-27 10:45:53,455 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:    26.368591, Tokens per Sec:    19360, Lr: 0.000300
2022-02-27 10:45:56,743 - INFO - joeynmt.training - Epoch  28: total training loss 5256.34
2022-02-27 10:45:56,743 - INFO - joeynmt.training - EPOCH 29
2022-02-27 10:45:59,000 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:    26.696507, Tokens per Sec:    19202, Lr: 0.000300
2022-02-27 10:46:04,673 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:    27.197027, Tokens per Sec:    19145, Lr: 0.000300
2022-02-27 10:46:07,611 - INFO - joeynmt.training - Epoch  29: total training loss 5222.24
2022-02-27 10:46:07,612 - INFO - joeynmt.training - EPOCH 30
2022-02-27 10:46:10,097 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:    27.575397, Tokens per Sec:    19492, Lr: 0.000300
2022-02-27 10:46:15,590 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:    27.157804, Tokens per Sec:    19731, Lr: 0.000300
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Epoch  30: total training loss 5177.38
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:   0.35 eval_metric.
2022-02-27 10:46:18,345 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 10:46:18,345 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 10:46:18,353 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:46:18,356 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:46:18,358 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 10:46:24,824 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.55 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:46:24,825 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 10:46:24,825 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 10:46:36,452 - INFO - joeynmt.prediction - test bleu[13a]:   0.76 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:46:36,453 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	5m59.273s
user	9m30.995s
sys	0m30.790s
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 34432.85938	PPL: 12.50890	bleu: 0.01036	LR: 0.00030000	*
Steps: 2000	Loss: 31097.80469	PPL: 9.79368	bleu: 0.01801	LR: 0.00030000	*
Steps: 3000	Loss: 29530.17773	PPL: 8.72957	bleu: 0.10866	LR: 0.00030000	*
Steps: 4000	Loss: 28522.73047	PPL: 8.10756	bleu: 0.27818	LR: 0.00030000	*
Steps: 5000	Loss: 27801.08008	PPL: 7.68944	bleu: 0.35137	LR: 0.00030000	*
```

တိုးတက်မှုတော့ ရှိတယ် bleu က တအားနည်းနေသေးတယ်...  

```
        hidden_size: 500 ပြန်ထားတယ် encoder အတွက်ရော decoder အတွက်ရော
        embedding_dim: 4096        ကိုလည်း encoder/decoder နှစ်ခုစလုံးအတွက် ထားခဲ့
```

train လုပ်ကြည့်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
...
...
...
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4124 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4123 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 11:57:03,712 - INFO - joeynmt.training - Epoch  26: total training loss 113.78
2022-02-27 11:57:03,712 - INFO - joeynmt.training - EPOCH 27
2022-02-27 11:57:27,124 - INFO - joeynmt.training - Epoch  27, Step:     5100, Batch Loss:     0.383438, Tokens per Sec:     1381, Lr: 0.000300
2022-02-27 11:58:42,233 - INFO - joeynmt.training - Epoch  27, Step:     5200, Batch Loss:     0.622168, Tokens per Sec:     1434, Lr: 0.000300
2022-02-27 11:59:31,602 - INFO - joeynmt.training - Epoch  27: total training loss 102.46
2022-02-27 11:59:31,602 - INFO - joeynmt.training - EPOCH 28
2022-02-27 11:59:58,982 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:     0.333518, Tokens per Sec:     1392, Lr: 0.000300
2022-02-27 12:01:15,597 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:     0.601976, Tokens per Sec:     1411, Lr: 0.000300
2022-02-27 12:02:00,380 - INFO - joeynmt.training - Epoch  28: total training loss 90.95
2022-02-27 12:02:00,380 - INFO - joeynmt.training - EPOCH 29
2022-02-27 12:02:30,506 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:     0.261766, Tokens per Sec:     1439, Lr: 0.000300
2022-02-27 12:03:48,839 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:     0.489499, Tokens per Sec:     1387, Lr: 0.000300
2022-02-27 12:04:29,301 - INFO - joeynmt.training - Epoch  29: total training loss 82.12
2022-02-27 12:04:29,301 - INFO - joeynmt.training - EPOCH 30
2022-02-27 12:05:03,715 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:     0.311833, Tokens per Sec:     1408, Lr: 0.000300
2022-02-27 12:06:19,441 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:     0.417136, Tokens per Sec:     1431, Lr: 0.000300
2022-02-27 12:06:56,702 - INFO - joeynmt.training - Epoch  30: total training loss 71.23
2022-02-27 12:06:56,703 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 12:06:56,703 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  82.32 eval_metric.
2022-02-27 12:06:56,731 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 12:06:56,731 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 12:06:57,278 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 12:06:57,671 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 12:06:57,760 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 12:07:40,696 - INFO - joeynmt.prediction -  dev bleu[13a]:  82.53 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 12:07:40,697 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 12:07:40,697 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 12:08:58,696 - INFO - joeynmt.prediction - test bleu[13a]:  81.63 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 12:08:58,697 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	78m29.084s
user	91m54.679s
sys	15m15.880s
```

အထက်မှာ မြင်ရတဲ့အတိုင်း... ဒီတစ်ခါတော့ RNN model က ငါတို့ရဲ့ မြန်မာ-ရခိုင် ဒေတာနဲ့ ကောင်းကောင်း အလုပ်လုပ်ပေးတယ်လို့ နားလည်တယ်။  
validation log ဖိုင်ကို ဝင်ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 5521.56543	PPL: 1.49950	bleu: 70.71308	LR: 0.00030000	*
Steps: 2000	Loss: 3119.77002	PPL: 1.25722	bleu: 80.89377	LR: 0.00030000	*
Steps: 3000	Loss: 2918.38110	PPL: 1.23878	bleu: 82.31551	LR: 0.00030000	*
Steps: 4000	Loss: 3539.79443	PPL: 1.29657	bleu: 81.79033	LR: 0.00030000	
Steps: 5000	Loss: 3400.03296	PPL: 1.28335	bleu: 82.32466	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt$ 
```

လက်ရှိ ပထမဆုံး ရလဒ်ကောင်း၊ သုံးလို့ ရနိုင်လို့ backup ကူးထားခဲ့...  

```
(joey) ye@:~/exp/joeynmt/models$ mv wmt_myrk_default/ wmt_myrk_default1
```

Beam Size ကို တိုးကြည့်မယ်။   

```
testing:
    beam_size: 10 # original setting is 5
    
        hidden_size: 1000 # encoder, decoder နှစ်မျိုးစလုံးအတွက်
```


run ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
2022-02-27 12:35:29,616 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 12:35:29,636 - INFO - joeynmt.data - Loading training data...
2022-02-27 12:35:32,624 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 12:35:32,703 - INFO - joeynmt.data - Loading dev data...
2022-02-27 12:35:32,726 - INFO - joeynmt.data - Loading test data...
2022-02-27 12:35:32,747 - INFO - joeynmt.data - Data loaded.
2022-02-27 12:35:32,747 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 12:35:33,505 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 12:35:33.773895: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-27 12:35:34,955 - INFO - joeynmt.training - Total params: 88247632
2022-02-27 12:35:34,956 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                           cfg.name : wmt_myrk_default
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 50
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 10
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0003
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 5e-07
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -            cfg.training.batch_size : 80
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.training.patience : 10
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                cfg.training.epochs : 30
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt_myrk_default
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 5
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 4096
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 1000
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 4096
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -        cfg.model.decoder.emb_scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 1000
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : bridge
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Data set sizes: 
	train 15535,
	valid 1000,
	test 1811
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Number of Src words (types): 1580
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Number of Trg words (types): 1687
2022-02-27 12:35:37,362 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(4096, 1000, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(5096, 1000, batch_first=True), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=4096, vocab_size=1580),
	trg_embed=Embeddings(embedding_dim=4096, vocab_size=1687))
2022-02-27 12:35:37,363 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 40
	total batch size (w. parallel & accumulation): 80
2022-02-27 12:35:37,363 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 447, in train_and_validate
    batch_loss += self._train_step(batch)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 539, in _train_step
    batch_loss, _, _, _ = self.model(return_type="loss", **vars(batch))
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 168, in forward
    outputs = self.parallel_apply(replicas, inputs, kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 178, in parallel_apply
    return parallel_apply(replicas, inputs, kwargs, self.device_ids[:len(replicas)])
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 86, in parallel_apply
    output.reraise()
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_utils.py", line 434, in reraise
    raise exception
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 98.00 MiB (GPU 1; 3.95 GiB total capacity; 3.00 GiB already allocated; 97.94 MiB free; 3.14 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m12.427s
user	0m6.328s
sys	0m2.620s
(joey) ye@:~/exp/joeynmt$ 
```

အထက်ပါအတိုင်း out of memory error တက်တယ်။  
အဲဒါကြောင့် hidden_size ကို 600 (100 ပဲ တိုးခဲ့) ပဲထားပြီး beam size ကိုတော့ 10 ပဲ ထားပြီး ထပ် training လုပ်ကြည့်ခဲ့...  

```
       hidden_size: 600
       beam_size: 10 # original setting is 5       
```

training again ... 

```
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 52.00 MiB (GPU 1; 3.95 GiB total capacity; 2.94 GiB already allocated; 40.94 MiB free; 3.18 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m39.949s
user	0m39.533s
sys	0m8.476s
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါအတိုင်း error ပေးပြီး training ရပ်သွားလို့... beam size ကိုလျှော့ပြီး ပြန် train လုပ်ကြည့်ခဲ့...  

```
       hidden_size: 600
       
testing:
    beam_size: 5 # original setting is 5
```

training လုပ်ခဲ့....  

```
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 168, in forward
    outputs = self.parallel_apply(replicas, inputs, kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 178, in parallel_apply
    return parallel_apply(replicas, inputs, kwargs, self.device_ids[:len(replicas)])
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 86, in parallel_apply
    output.reraise()
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_utils.py", line 434, in reraise
    raise exception
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 52.00 MiB (GPU 1; 3.95 GiB total capacity; 2.94 GiB already allocated; 40.94 MiB free; 3.18 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m38.592s
user	0m40.241s
sys	0m8.479s
(joey) ye@:~/exp/joeynmt$ 
```

လက်ရှိ စက်နဲ့က မနိုင်ဘူး... 
အဲဒါကြောင့် ... နောက်ထပ် အရေးကြီးတဲ့ parameter တစ်ခု ဖြစ်တဲ့ hidden layer ကိုပဲ တိုးကြည့်မယ်။  

```
        num_layers: 2 # 1 ကနေ 2 အထိ တင်ကြည့်ခဲ့...  
```

run ကြည့်ခဲ့...  

```
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 50.00 MiB (GPU 1; 3.95 GiB total capacity; 2.95 GiB already allocated; 16.94 MiB free; 3.21 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m38.850s
user	0m40.468s
sys	0m8.179s
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါအတိုင်း error ပေးတယ်။ ဒီတစ်ခါတော့ hidden layer ကို 2 ထားထားပြီး hidden_size ကို 300 ထားကြည့်မယ်...  

```
        num_layers: 2
        hidden_size: 300 # for both encoder/decoder        
```

training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 13:56:56,670 - INFO - joeynmt.training - EPOCH 28
2022-02-27 13:57:16,583 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:     0.835923, Tokens per Sec:     1914, Lr: 0.000300
2022-02-27 13:58:12,621 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:     1.400406, Tokens per Sec:     1929, Lr: 0.000300
2022-02-27 13:58:45,413 - INFO - joeynmt.training - Epoch  28: total training loss 210.51
2022-02-27 13:58:45,414 - INFO - joeynmt.training - EPOCH 29
2022-02-27 13:59:07,497 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:     0.650256, Tokens per Sec:     1963, Lr: 0.000300
2022-02-27 14:00:05,073 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:     1.080434, Tokens per Sec:     1886, Lr: 0.000300
2022-02-27 14:00:34,237 - INFO - joeynmt.training - Epoch  29: total training loss 192.59
2022-02-27 14:00:34,237 - INFO - joeynmt.training - EPOCH 30
2022-02-27 14:00:59,486 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:     1.102342, Tokens per Sec:     1918, Lr: 0.000300
2022-02-27 14:01:54,616 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:     0.951962, Tokens per Sec:     1966, Lr: 0.000300
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Epoch  30: total training loss 179.17
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  82.33 eval_metric.
2022-02-27 14:02:22,170 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 14:02:22,171 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 14:02:22,576 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 14:02:22,862 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 14:02:22,917 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 14:02:54,819 - INFO - joeynmt.prediction -  dev bleu[13a]:  82.53 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 14:02:54,821 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 14:02:54,821 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 14:03:51,285 - INFO - joeynmt.prediction - test bleu[13a]:  81.19 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 14:03:51,289 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	58m25.911s
user	71m45.595s
sys	9m6.336s
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 19013.80859	PPL: 4.03538	bleu: 14.87704	LR: 0.00030000	*
Steps: 2000	Loss: 7608.55371	PPL: 1.74763	bleu: 58.67979	LR: 0.00030000	*
Steps: 3000	Loss: 3492.30786	PPL: 1.29206	bleu: 79.77457	LR: 0.00030000	*
Steps: 4000	Loss: 3101.71558	PPL: 1.25556	bleu: 81.94242	LR: 0.00030000	*
Steps: 5000	Loss: 3153.44263	PPL: 1.26033	bleu: 82.32911	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါ မော်ဒယ်လည်း သုံးလို့ ရလိမ့်မယ်။  
backup ကူးထားခဲ့...  

## Training with wmt_myrk_best.yaml

```
(joey) ye@:~/exp/joeynmt/configs$ cat ./wmt_myrk_best.yaml 
name: "wmt_myrk_best"

data:
    src: "my"
    trg: "rk"
    train: "/media/ye/project2/exp/myrk-transformer/data/syl/train"    # training data
    dev: "/media/ye/project2/exp/myrk-transformer/data/syl/dev"        # development data for validation
    test: "/media/ye/project2/exp/myrk-transformer/data/syl/test"      # test data for testing final model; optional    
    level: "word"
    lowercase: False
    max_sent_length: 100
    src_voc_min_freq: 0
    src_voc_limit: 100000
    trg_voc_min_freq: 0
    trg_voc_limit: 100000
    #src_vocab: "test/data/en-de/vocab.txt"
    #trg_vocab: "test/data/en-de/vocab.txt"

testing:
    beam_size: 5
    alpha: 1.0

training:
    random_seed: 42
    optimizer: "adam"
    learning_rate: 0.0002
    learning_rate_min: 0.0000005
    weight_decay: 0.0
    clip_grad_norm: 1.0
    batch_size: 4096
    batch_type: "token"
    scheduling: "plateau"
    patience: 4
    decrease_factor: 0.7
    early_stopping_metric: "ppl"
    epochs: 20
    validation_freq: 8000
    logging_freq: 1000
    eval_metric: "bleu"
    model_dir: "models/wmt_myrk_best"
    overwrite: False
    shuffle: True
    use_cuda: True
    max_output_length: 100
    print_valid_sents: [0, 1, 2]

model:
    tied_embeddings: True
    encoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 512
            scale: False
        hidden_size: 300
        bidirectional: True
        dropout: 0.2
        num_layers: 2
    decoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 512
            scale: False
        emb_scale: False
        hidden_size: 300
        dropout: 0.2
        hidden_dropout: 0.2
        num_layers: 2
        input_feeding: True
        init_hidden: "bridge"
        attention: "bahdanau"
(joey) ye@:~/exp/joeynmt/configs$
```

training start ...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_best.yaml 
2022-02-27 14:13:55,689 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 14:13:55,711 - INFO - joeynmt.data - Loading training data...
2022-02-27 14:13:58,606 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 14:13:58,683 - INFO - joeynmt.data - Loading dev data...
2022-02-27 14:13:58,709 - INFO - joeynmt.data - Loading test data...
2022-02-27 14:13:58,762 - INFO - joeynmt.data - Data loaded.
2022-02-27 14:13:58,762 - INFO - joeynmt.model - Building an encoder-decoder model...
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 820, in train
    model = build_model(cfg["model"], src_vocab=src_vocab, trg_vocab=trg_vocab)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 225, in build_model
    raise ConfigurationError(
joeynmt.helpers.ConfigurationError: Embedding cannot be tied since vocabularies differ.

real	0m5.015s
user	0m1.451s
sys	0m0.741s
(joey) ye@:~/exp/joeynmt$ 

```

config ဖိုင်ကို ပြန်စစ်ကြည့်....  
    tied_embeddings: True ဆိုတဲ့ setting ကြောင့် ပေးတဲ့ error ... လို့ ထင်တယ်။  
    တကယ်ကတော့ မြန်မာ နဲ့ ရခိုင်က syllable ဆိုရင် tied လုပ်လို့ ရနိုင်တယ်။ လက်တွေ့ ဒေတာက နည်းတော့ တဖက်မှာ ရှိတဲ့ syllable က နောက်တစ်ဖက်မှာ မရှိတဲ့ ပြဿနာကြောင့်လို့ ယူဆခဲ့...  
 
```
    lowercase: True
    #load_model: "models/small_model/60.ckpt" # if given, load a pre-trained model from this checkpoint
    reset_best_ckpt: False          # if True, reset the tracking of the best checkpoint and scores. Use for domain adaptation or fine-tuning with new metrics or dev data.
    reset_scheduler: False          # if True, overwrite scheduler in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.
    reset_optimizer: False          # if True, overwrite optimizer in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.    
    
        tied_embeddings: False
```

နောက်တစ်ခေါက် training လုပ်ခဲ့...  

```
2022-02-27 15:00:58,694 - INFO - joeynmt.training - Epoch  20, Step:     3000, Batch Loss:    15.104771, Tokens per Sec:     4933, Lr: 0.000200
2022-02-27 15:01:23,449 - INFO - joeynmt.training - Epoch  20: total training loss 2494.04
2022-02-27 15:01:23,449 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-27 15:01:23,449 - INFO - joeynmt.training - Best validation result (greedy) at step        0:    inf ppl.
2022-02-27 15:01:23,470 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 2048
2022-02-27 15:01:23,470 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_best/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint models/wmt_myrk_best/0.ckpt not found

real	14m31.977s
user	19m39.879s
sys	1m55.105s
(joey) ye@:~/exp/joeynmt$ 

```

default config တုန်းကလို same error တက်ခဲ့...  
batch size ကို default ထက် +20 ပြောင်းလိုက် ပြီး training ထပ်လုပ်ကြည့်ခဲ့ ...  

```
    batch_size: 100
```

training start ...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_best.yaml
...
...
...

/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4124 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4123 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 17:21:21,421 - INFO - joeynmt.training - Epoch  18: total training loss 5727.35
2022-02-27 17:21:21,422 - INFO - joeynmt.training - EPOCH 19
2022-02-27 17:21:58,612 - INFO - joeynmt.training - Epoch  19, Step:    65000, Batch Loss:     0.590321, Tokens per Sec:      531, Lr: 0.000200
2022-02-27 17:23:47,195 - INFO - joeynmt.training - Epoch  19, Step:    66000, Batch Loss:     0.107867, Tokens per Sec:      543, Lr: 0.000200
2022-02-27 17:25:36,711 - INFO - joeynmt.training - Epoch  19, Step:    67000, Batch Loss:     0.601114, Tokens per Sec:      533, Lr: 0.000200
2022-02-27 17:27:26,626 - INFO - joeynmt.training - Epoch  19, Step:    68000, Batch Loss:     2.223678, Tokens per Sec:      534, Lr: 0.000200
2022-02-27 17:27:54,985 - INFO - joeynmt.training - Epoch  19: total training loss 5203.92
2022-02-27 17:27:54,985 - INFO - joeynmt.training - EPOCH 20
2022-02-27 17:29:15,252 - INFO - joeynmt.training - Epoch  20, Step:    69000, Batch Loss:     2.569880, Tokens per Sec:      543, Lr: 0.000200
2022-02-27 17:31:04,769 - INFO - joeynmt.training - Epoch  20, Step:    70000, Batch Loss:     0.235845, Tokens per Sec:      538, Lr: 0.000200
2022-02-27 17:32:53,855 - INFO - joeynmt.training - Epoch  20, Step:    71000, Batch Loss:     3.569670, Tokens per Sec:      540, Lr: 0.000200
2022-02-27 17:34:26,413 - INFO - joeynmt.training - Epoch  20: total training loss 4710.98
2022-02-27 17:34:26,413 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-27 17:34:26,413 - INFO - joeynmt.training - Best validation result (greedy) at step    48000:   1.28 ppl.
2022-02-27 17:34:26,438 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 50
2022-02-27 17:34:26,438 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_best/48000.ckpt
2022-02-27 17:34:26,556 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 17:34:26,634 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 17:34:26,659 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 17:36:08,050 - INFO - joeynmt.prediction -  dev bleu[13a]:  83.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 17:36:08,051 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_best/00048000.hyps.dev
2022-02-27 17:36:08,051 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 17:39:15,225 - INFO - joeynmt.prediction - test bleu[13a]:  80.72 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 17:39:15,226 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_best/00048000.hyps.test

real	142m22.083s
user	190m7.548s
sys	3m44.667s

```

validation log ဖိုင်ကိုလည်း ကြည့်ခဲ့...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_best/validations.txt 
Steps: 8000	Loss: 18146.52148	PPL: 3.78658	bleu: 18.84207	LR: 0.00020000	*
Steps: 16000	Loss: 5441.65430	PPL: 1.49074	bleu: 71.60242	LR: 0.00020000	*
Steps: 24000	Loss: 4119.06348	PPL: 1.35287	bleu: 79.25485	LR: 0.00020000	*
Steps: 32000	Loss: 3592.66162	PPL: 1.30161	bleu: 80.07143	LR: 0.00020000	*
Steps: 40000	Loss: 3564.08643	PPL: 1.29889	bleu: 81.59423	LR: 0.00020000	*
Steps: 48000	Loss: 3382.44775	PPL: 1.28169	bleu: 82.63535	LR: 0.00020000	*
Steps: 56000	Loss: 3466.66016	PPL: 1.28963	bleu: 82.88525	LR: 0.00020000	
Steps: 64000	Loss: 3491.84253	PPL: 1.29202	bleu: 82.98669	LR: 0.00020000	
(joey) ye@:~/exp/joeynmt$
```

## Transformer Model Training

```
(joey) ye@:~/exp/joeynmt/configs$ cp transformer_wmt17_ende.yaml transformer_wmt17_myrk.yaml 
```

training ...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_ 
wmt_myrk_best.yaml     wmt_myrk_default.yaml  
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/transformer_wmt17_myrk.yaml 
2022-02-27 18:26:50,301 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 18:26:50,319 - INFO - joeynmt.data - Loading training data...
2022-02-27 18:26:53,264 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 18:26:53,340 - INFO - joeynmt.data - Loading dev data...
2022-02-27 18:26:53,387 - INFO - joeynmt.data - Loading test data...
2022-02-27 18:26:53,407 - INFO - joeynmt.data - Data loaded.
2022-02-27 18:26:53,407 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 18:26:53,845 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 18:26:54.116603: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-27 18:26:55,331 - INFO - joeynmt.training - Total params: 46688768
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                           cfg.name : transformer_myrk
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 100
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -         cfg.training.normalization : tokens
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -            cfg.training.adam_betas : [0.9, 0.999]
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -              cfg.training.patience : 8
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.7
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                  cfg.training.loss : crossentropy
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0002
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 1e-08
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -       cfg.training.label_smoothing : 0.1
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -            cfg.training.batch_size : 80
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -            cfg.training.batch_type : token
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -       cfg.training.eval_batch_size : 80
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -       cfg.training.eval_batch_type : token
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -      cfg.training.batch_multiplier : 1
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : ppl
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -                cfg.training.epochs : 100
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt17_myrk_transformer
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -             cfg.training.overwrite : False
2022-02-27 18:26:57,641 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2, 3]
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 5
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -                cfg.model.init_gain : 1.0
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : xavier
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.embed_init_gain : 1.0
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.tied_embeddings : False
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -             cfg.model.tied_softmax : False
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -             cfg.model.encoder.type : transformer
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 6
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -        cfg.model.encoder.num_heads : 8
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 512
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : True
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.dropout : 0.0
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 512
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.encoder.ff_size : 2048
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -             cfg.model.decoder.type : transformer
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 6
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -        cfg.model.decoder.num_heads : 8
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 512
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : True
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.dropout : 0.0
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 512
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.decoder.ff_size : 2048
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - Data set sizes: 
	train 15561,
	valid 1000,
	test 1811
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-02-27 18:26:57,642 - INFO - joeynmt.helpers - Number of Src words (types): 1587
2022-02-27 18:26:57,643 - INFO - joeynmt.helpers - Number of Trg words (types): 1695
2022-02-27 18:26:57,643 - INFO - joeynmt.training - Model(
	encoder=TransformerEncoder(num_layers=6, num_heads=8),
	decoder=TransformerDecoder(num_layers=6, num_heads=8),
	src_embed=Embeddings(embedding_dim=512, vocab_size=1587),
	trg_embed=Embeddings(embedding_dim=512, vocab_size=1695))
2022-02-27 18:26:57,644 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 40
	total batch size (w. parallel & accumulation): 80
2022-02-27 18:26:57,644 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 18:27:22,120 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:     1.736905, Tokens per Sec:      197, Lr: 0.000200
2022-02-27 18:27:44,974 - INFO - joeynmt.training - Epoch   1, Step:      200, Batch Loss:     1.887940, Tokens per Sec:      216, Lr: 0.000200
2022-02-27 18:28:07,501 - INFO - joeynmt.training - Epoch   1, Step:      300, Batch Loss:     1.801592, Tokens per Sec:      218, Lr: 0.000200
2022-02-27 18:28:30,416 - INFO - joeynmt.training - Epoch   1, Step:      400, Batch Loss:     1.493442, Tokens per Sec:      209, Lr: 0.000200
2022-02-27 18:28:52,985 - INFO - joeynmt.training - Epoch   1, Step:      500, Batch Loss:     2.170482, Tokens per Sec:      215, Lr: 0.000200
2022-02-27 18:29:15,465 - INFO - joeynmt.training - Epoch   1, Step:      600, Batch Loss:     1.580761, Tokens per Sec:      216, Lr: 0.000200
2022-02-27 18:29:38,183 - INFO - joeynmt.training - Epoch   1, Step:      700, Batch Loss:     1.206359, Tokens per Sec:      210, Lr: 0.000200
2022-02-27 18:30:00,644 - INFO - joeynmt.training - Epoch   1, Step:      800, Batch Loss:     1.859487, Tokens per Sec:      209, Lr: 0.000200
2022-02-27 18:30:23,522 - INFO - joeynmt.training - Epoch   1, Step:      900, Batch Loss:     1.986260, Tokens per Sec:      210, Lr: 0.000200
2022-02-27 18:30:46,125 - INFO - joeynmt.training - Epoch   1, Step:     1000, Batch Loss:     1.429042, Tokens per Sec:      211, Lr: 0.000200
2022-02-27 18:46:14,058 - INFO - joeynmt.training - Hooray! New best validation result [ppl]!
2022-02-27 18:46:14,673 - INFO - joeynmt.training - Example #0
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Hypothesis: မင်း အ တွက် အ တွက် အ တွက် ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - Example #1
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Hypothesis: ကျွန် တော် ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ရို့ ကတ် ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - Example #2
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - 	Hypothesis: ငါ ရို့ လာ လား ရေ ။
2022-02-27 18:46:14,674 - INFO - joeynmt.training - Example #3
2022-02-27 18:46:14,675 - INFO - joeynmt.training - 	Source:     မင်း ဘာ တွေ ပြန် စဉ်း စား နေ သ လဲ ဆို တာ ငါ့ ကို ပြော ပြ စမ်း ပါ ဦး ။
2022-02-27 18:46:14,675 - INFO - joeynmt.training - 	Reference:  မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-27 18:46:14,675 - INFO - joeynmt.training - 	Hypothesis: မင်း ဇာ သူ့ ကို ဇာ ပိုင် ဆို စွာ မင်း ဇာ ပိုင် ဆို စွာ လေး ။
2022-02-27 18:46:14,675 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     1000: bleu:   5.34, loss: 20392.8281, ppl:   4.4651, duration: 928.5499s
2022-02-27 18:46:37,322 - INFO - joeynmt.training - Epoch   1, Step:     1100, Batch Loss:     1.617543, Tokens per Sec:      217, Lr: 0.000200
2022-02-27 18:47:00,652 - INFO - joeynmt.training - Epoch   1, Step:     1200, Batch Loss:     1.387858, Tokens per Sec:      205, Lr: 0.000200
2022-02-27 18:47:23,937 - INFO - joeynmt.training - Epoch   1, Step:     1300, Batch Loss:     1.447458, Tokens per Sec:      201, Lr: 0.000200
2022-02-27 18:47:46,926 - INFO - joeynmt.training - Epoch   1, Step:     1400, Batch Loss:     1.020369, Tokens per Sec:      202, Lr: 0.000200
2022-02-27 18:48:09,956 - INFO - joeynmt.training - Epoch   1, Step:     1500, Batch Loss:     1.507658, Tokens per Sec:      212, Lr: 0.000200
2022-02-27 18:48:33,359 - INFO - joeynmt.training - Epoch   1, Step:     1600, Batch Loss:     1.042174, Tokens per Sec:      205, Lr: 0.000200
2022-02-27 18:48:56,070 - INFO - joeynmt.training - Epoch   1, Step:     1700, Batch Loss:     0.671704, Tokens per Sec:      211, Lr: 0.000200
2022-02-27 18:49:18,874 - INFO - joeynmt.training - Epoch   1, Step:     1800, Batch Loss:     1.282546, Tokens per Sec:      209, Lr: 0.000200
2022-02-27 18:49:41,037 - INFO - joeynmt.training - Epoch   1, Step:     1900, Batch Loss:     1.197685, Tokens per Sec:      208, Lr: 0.000200
2022-02-27 18:50:04,099 - INFO - joeynmt.training - Epoch   1, Step:     2000, Batch Loss:     1.537325, Tokens per Sec:      212, Lr: 0.000200

...
...
...
2022-02-27 19:39:53,906 - INFO - joeynmt.training - Epoch   2, Step:     5100, Batch Loss:     0.727085, Tokens per Sec:      216, Lr: 0.000200
2022-02-27 19:40:16,387 - INFO - joeynmt.training - Epoch   2, Step:     5200, Batch Loss:     0.657699, Tokens per Sec:      213, Lr: 0.000200
2022-02-27 19:40:38,796 - INFO - joeynmt.training - Epoch   2, Step:     5300, Batch Loss:     0.424888, Tokens per Sec:      209, Lr: 0.000200
2022-02-27 19:41:01,617 - INFO - joeynmt.training - Epoch   2, Step:     5400, Batch Loss:     0.384180, Tokens per Sec:      215, Lr: 0.000200
2022-02-27 19:41:24,478 - INFO - joeynmt.training - Epoch   2, Step:     5500, Batch Loss:     0.621914, Tokens per Sec:      217, Lr: 0.000200
2022-02-27 19:41:47,195 - INFO - joeynmt.training - Epoch   2, Step:     5600, Batch Loss:     0.531037, Tokens per Sec:      206, Lr: 0.000200
2022-02-27 19:42:09,835 - INFO - joeynmt.training - Epoch   2, Step:     5700, Batch Loss:     0.269372, Tokens per Sec:      218, Lr: 0.000200
2022-02-27 19:42:32,652 - INFO - joeynmt.training - Epoch   2, Step:     5800, Batch Loss:     0.769344, Tokens per Sec:      212, Lr: 0.000200
2022-02-27 19:42:54,619 - INFO - joeynmt.training - Epoch   2, Step:     5900, Batch Loss:     0.411499, Tokens per Sec:      214, Lr: 0.000200
2022-02-27 19:43:17,252 - INFO - joeynmt.training - Epoch   2, Step:     6000, Batch Loss:     0.434516, Tokens per Sec:      216, Lr: 0.000200
2022-02-27 19:50:34,760 - INFO - joeynmt.training - Hooray! New best validation result [ppl]!
2022-02-27 19:50:35,371 - INFO - joeynmt.helpers - delete models/wmt17_myrk_transformer/1000.ckpt
2022-02-27 19:50:35,373 - INFO - joeynmt.training - Example #0
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Hypothesis: မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 19:50:35,373 - INFO - joeynmt.training - Example #1
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-27 19:50:35,373 - INFO - joeynmt.training - 	Hypothesis: ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ဖို့ ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - Example #2
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Hypothesis: စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - Example #3
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Source:     မင်း ဘာ တွေ ပြန် စဉ်း စား နေ သ လဲ ဆို တာ ငါ့ ကို ပြော ပြ စမ်း ပါ ဦး ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Reference:  မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - 	Hypothesis: မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ လိုက် ပါ ။
2022-02-27 19:50:35,374 - INFO - joeynmt.training - Validation result (greedy) at epoch   2, step     6000: bleu:  51.88, loss: 8321.2246, ppl:   1.8414, duration: 438.1216s
2022-02-27 19:50:58,470 - INFO - joeynmt.training - Epoch   2, Step:     6100, Batch Loss:     0.375760, Tokens per Sec:      214, Lr: 0.000200
2022-02-27 19:51:21,498 - INFO - joeynmt.training - Epoch   2, Step:     6200, Batch Loss:     0.713445, Tokens per Sec:      203, Lr: 0.000200
...
...
...
, duration: 433.5684s
2022-02-27 21:19:41,606 - INFO - joeynmt.training - Epoch   4, Step:    14100, Batch Loss:     0.208562, Tokens per Sec:      225, Lr: 0.000200
2022-02-27 21:20:04,618 - INFO - joeynmt.training - Epoch   4, Step:    14200, Batch Loss:     0.374840, Tokens per Sec:      212, Lr: 0.000200
2022-02-27 21:20:28,051 - INFO - joeynmt.training - Epoch   4, Step:    14300, Batch Loss:     0.137479, Tokens per Sec:      206, Lr: 0.000200
2022-02-27 21:20:50,818 - INFO - joeynmt.training - Epoch   4, Step:    14400, Batch Loss:     0.283308, Tokens per Sec:      214, Lr: 0.000200
2022-02-27 21:21:13,785 - INFO - joeynmt.training - Epoch   4, Step:    14500, Batch Loss:     0.100229, Tokens per Sec:      206, Lr: 0.000200
2022-02-27 21:21:36,694 - INFO - joeynmt.training - Epoch   4, Step:    14600, Batch Loss:     0.380258, Tokens per Sec:      203, Lr: 0.000200
2022-02-27 21:21:59,220 - INFO - joeynmt.training - Epoch   4, Step:    14700, Batch Loss:     0.618619, Tokens per Sec:      213, Lr: 0.000200
2022-02-27 21:22:21,767 - INFO - joeynmt.training - Epoch   4, Step:    14800, Batch Loss:     0.314114, Tokens per Sec:      215, Lr: 0.000200
2022-02-27 21:22:44,938 - INFO - joeynmt.training - Epoch   4, Step:    14900, Batch Loss:     0.469316, Tokens per Sec:      208, Lr: 0.000200
2022-02-27 21:23:08,525 - INFO - joeynmt.training - Epoch   4, Step:    15000, Batch Loss:     1.086011, Tokens per Sec:      210, Lr: 0.000200
2022-02-27 21:30:32,349 - INFO - joeynmt.training - Hooray! New best validation result [ppl]!
2022-02-27 21:30:33,011 - INFO - joeynmt.helpers - delete models/wmt17_myrk_transformer/10000.ckpt
2022-02-27 21:30:33,013 - INFO - joeynmt.training - Example #0
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Hypothesis: မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - Example #1
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Hypothesis: ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မယ် ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - Example #2
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Hypothesis: စာ အုပ် ဝယ် ဖို့ မိ လား ရေ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - Example #3
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Source:     မင်း ဘာ တွေ ပြန် စဉ်း စား နေ သ လဲ ဆို တာ ငါ့ ကို ပြော ပြ စမ်း ပါ ဦး ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Reference:  မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - 	Hypothesis: မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-27 21:30:33,014 - INFO - joeynmt.training - Validation result (greedy) at epoch   4, step    15000: bleu:  64.55, loss: 6183.0083, ppl:   1.5741, duration: 444.4885s
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 441, in train_and_validate
    for i, batch in enumerate(iter(self.train_iter)):
  File "/home/ye/.local/lib/python3.8/site-packages/torchtext/legacy/data/iterator.py", line 160, in __iter__
    yield Batch(minibatch, self.dataset, self.device)
  File "/home/ye/.local/lib/python3.8/site-packages/torchtext/legacy/data/batch.py", line 34, in __init__
    setattr(self, name, field.process(batch, device=device))
  File "/home/ye/.local/lib/python3.8/site-packages/torchtext/legacy/data/field.py", line 230, in process
    padded = self.pad(batch)
  File "/home/ye/.local/lib/python3.8/site-packages/torchtext/legacy/data/field.py", line 248, in pad
    max_len = max(len(x) for x in minibatch)
ValueError: max() arg is an empty sequence

real	184m0.895s
user	311m51.850s
sys	5m15.896s
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါအတိုင်း ERROR တက်တယ်...  

(joey) ye@:~/exp/joeynmt$ gedit /home/ye/.local/lib/python3.8/site-packages/torchtext/legacy/data/field.py ဖိုင် က ပေးတဲ့ error မို့လို့ code ကို ကြည့်တော့...  

```python
        Pads to self.fix_length if provided, otherwise pads to the length of
        the longest example in the batch. Prepends self.init_token and appends
        self.eos_token if those attributes are not None. Returns a tuple of the
        padded list and a list containing lengths of each example if
        `self.include_lengths` is `True` and `self.sequential` is `True`, else just
        returns the padded list. If `self.sequential` is `False`, no padding is applied.
        """
        minibatch = list(minibatch)
        if not self.sequential:
            return minibatch
        if self.fix_length is None:
            max_len = max(len(x) for x in minibatch)
        else:
            max_len = self.fix_length + (
                self.init_token, self.eos_token).count(None) - 2
```

reference: https://github.com/OpenNMT/OpenNMT-py/issues/1003  
I find it is the problem that you set the batch_size =2 and batch_type=tokens.The batch_size should be 4096 or some values are bigger enough.The same error occurs when i set the batch_size=32 and batch_type=tokens.

batch_size ကို များများ ပြန်ထားကြည့်ခဲ့...  
အောက်ပါအတိုင်း config ဖိုင်ကို ဝင်ပြင်ပြီး နောက်တစ်ခေါက် ထပ် training လုပ်ခဲ့...  

```
    batch_size: 4096
    batch_type: "token"
    eval_batch_size: 4096
    eval_batch_type: "token"
```

training ပြန်လုပ်ကြည့်ခဲ့...  

```
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/transformer_layers.py", line 54, in forward
    k = self.k_layer(k)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/linear.py", line 103, in forward
    return F.linear(input, self.weight, self.bias)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/functional.py", line 1848, in linear
    return torch._C._nn.linear(input, weight, bias)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 1.59 GiB already allocated; 76.25 MiB free; 1.64 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m11.811s
user	0m6.987s
sys	0m2.410s
(joey) ye@:~/exp/joeynmt$ 
ဋ  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/transformer_layers.py", line 54, in forward
    k = self.k_layer(k)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/linear.py", line 103, in forward
    return F.linear(input, self.weight, self.bias)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/functional.py", line 1848, in linear
    return torch._C._nn.linear(input, weight, bias)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 1.59 GiB already allocated; 76.25 MiB free; 1.64 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m11.811s
user	0m6.987s
sys	0m2.410s
(joey) ye@:~/exp/joeynmt$ 

```

memory မနိုင်ဘူး။ 128 ထားပြီး training ပြန်လုပ်ကြည့်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/transformer_wmt17_myrk.yaml 
...
...
...
2022-02-28 17:59:26,579 - INFO - joeynmt.training - Epoch  41, Step:   117000, Batch Loss:     0.029757, Tokens per Sec:      317, Lr: 0.000024
2022-02-28 18:05:03,861 - INFO - joeynmt.training - Example #0
2022-02-28 18:05:03,863 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-28 18:05:03,863 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-28 18:05:03,863 - INFO - joeynmt.training - 	Hypothesis: မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-28 18:05:03,863 - INFO - joeynmt.training - Example #1
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Hypothesis: ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - Example #2
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Hypothesis: စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - Example #3
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Source:     မင်း ဘာ တွေ ပြန် စဉ်း စား နေ သ လဲ ဆို တာ ငါ့ ကို ပြော ပြ စမ်း ပါ ဦး ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Reference:  မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - 	Hypothesis: မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-28 18:05:03,864 - INFO - joeynmt.training - Validation result (greedy) at epoch  41, step   117000: bleu:  81.04, loss: 3317.8389, ppl:   1.2756, duration: 337.2845s
2022-02-28 18:05:27,489 - INFO - joeynmt.training - Epoch  41, Step:   117100, Batch Loss:     0.016878, Tokens per Sec:      313, Lr: 0.000024
2022-02-28 18:05:51,038 - INFO - joeynmt.training - Epoch  41, Step:   117200, Batch Loss:     0.017180, Tokens per Sec:      301, Lr: 0.000024
2022-02-28 18:06:14,702 - INFO - joeynmt.training - Epoch  41, Step:   117300, Batch Loss:     0.028932, Tokens per Sec:      311, Lr: 0.000024
2022-02-28 18:06:38,225 - INFO - joeynmt.training - Epoch  41, Step:   117400, Batch Loss:     0.028456, Tokens per Sec:      314, Lr: 0.000024
2022-02-28 18:07:01,825 - INFO - joeynmt.training - Epoch  41, Step:   117500, Batch Loss:     0.020933, Tokens per Sec:      316, Lr: 0.000024
2022-02-28 18:07:25,437 - INFO - joeynmt.training - Epoch  41, Step:   117600, Batch Loss:     0.015796, Tokens per Sec:      308, Lr: 0.000024
2022-02-28 18:07:52,164 - INFO - joeynmt.training - Epoch  41, Step:   117700, Batch Loss:     0.024122, Tokens per Sec:      263, Lr: 0.000024
2022-02-28 18:08:15,315 - INFO - joeynmt.training - Epoch  41, Step:   117800, Batch Loss:     0.014571, Tokens per Sec:      312, Lr: 0.000024
2022-02-28 18:08:39,072 - INFO - joeynmt.training - Epoch  41, Step:   117900, Batch Loss:     0.013142, Tokens per Sec:      306, Lr: 0.000024
2022-02-28 18:09:02,707 - INFO - joeynmt.training - Epoch  41, Step:   118000, Batch Loss:     0.013039, Tokens per Sec:      299, Lr: 0.000024
2022-02-28 18:15:22,026 - INFO - joeynmt.training - Example #0
2022-02-28 18:15:22,033 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Hypothesis: မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - Example #1
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Hypothesis: ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - Example #2
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - 	Hypothesis: စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-28 18:15:22,034 - INFO - joeynmt.training - Example #3
2022-02-28 18:15:22,035 - INFO - joeynmt.training - 	Source:     မင်း ဘာ တွေ ပြန် စဉ်း စား နေ သ လဲ ဆို တာ ငါ့ ကို ပြော ပြ စမ်း ပါ ဦး ။
2022-02-28 18:15:22,035 - INFO - joeynmt.training - 	Reference:  မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-28 18:15:22,035 - INFO - joeynmt.training - 	Hypothesis: မင်း ဇာ တိ ပြန် စဉ်း စား နီ လေး ဆို စွာ ငါ့ ကို ပြော ပြ စမ်း ပါ ။
2022-02-28 18:15:22,035 - INFO - joeynmt.training - Validation result (greedy) at epoch  41, step   118000: bleu:  81.25, loss: 3304.4888, ppl:   1.2744, duration: 379.3273s
2022-02-28 18:15:47,284 - INFO - joeynmt.training - Epoch  41, Step:   118100, Batch Loss:     0.023462, Tokens per Sec:      297, Lr: 0.000024
2022-02-28 18:16:12,519 - INFO - joeynmt.training - Epoch  41, Step:   118200, Batch Loss:     0.018523, Tokens per Sec:      292, Lr: 0.000024
2022-02-28 18:16:36,722 - INFO - joeynmt.training - Epoch  41, Step:   118300, Batch Loss:     0.028439, Tokens per Sec:      309, Lr: 0.000024
2022-02-28 18:16:43,900 - INFO - joeynmt.training - Epoch  41: total training loss 77.51
2022-02-28 18:16:43,904 - INFO - joeynmt.training - EPOCH 42
2022-02-28 18:17:05,075 - INFO - joeynmt.training - Epoch  42, Step:   118400, Batch Loss:     0.019120, Tokens per Sec:      246, Lr: 0.000024
2022-02-28 18:17:29,142 - INFO - joeynmt.training - Epoch  42, Step:   118500, Batch Loss:     0.039711, Tokens per Sec:      308, Lr: 0.000024
2022-02-28 18:17:52,868 - INFO - joeynmt.training - Epoch  42, Step:   118600, Batch Loss:     0.022110, Tokens per Sec:      315, Lr: 0.000024
2022-02-28 18:18:16,708 - INFO - joeynmt.training - Epoch  42, Step:   118700, Batch Loss:     0.026570, Tokens per Sec:      305, Lr: 0.000024
2022-02-28 18:18:40,408 - INFO - joeynmt.training - Epoch  42, Step:   118800, Batch Loss:     0.022048, Tokens per Sec:      302, Lr: 0.000024
2022-02-28 18:19:04,188 - INFO - joeynmt.training - Epoch  42, Step:   118900, Batch Loss:     0.018201, Tokens per Sec:      300, Lr: 0.000024
2022-02-28 18:19:27,976 - INFO - joeynmt.training - Epoch  42, Step:   119000, Batch Loss:     0.026365, Tokens per Sec:      307, Lr: 0.000024
Killed

real	1151m15.818s
user	1873m57.938s
sys	34m48.140s

```

Killed ဖြစ်သွားတယ် ဆိုတာကိုတော့ တွေ့ရ...  
မော်ဒယ် folder ကို ဝင်ကြည့်...  

```
(joey) ye@:~/exp/joeynmt/models/wmt17_myrk_transformer$ ls
100000.hyps  108000.hyps  118000.hyps  21000.hyps  31000.hyps  41000.hyps  51000.hyps  61000.hyps  71000.hyps  8000.hyps   90000.hyps  98000.hyps
10000.hyps   109000.hyps  12000.hyps   22000.hyps  32000.hyps  42000.hyps  52000.hyps  62000.hyps  72000.hyps  81000.hyps  9000.hyps   99000.hyps
1000.hyps    110000.hyps  13000.hyps   23000.hyps  33000.hyps  43000.hyps  53000.hyps  63000.hyps  73000.hyps  82000.hyps  91000.ckpt  best.ckpt
101000.hyps  11000.hyps   14000.hyps   24000.hyps  34000.hyps  44000.hyps  54000.hyps  64000.hyps  74000.hyps  83000.hyps  91000.hyps  config.yaml
102000.ckpt  111000.hyps  15000.hyps   25000.hyps  35000.hyps  45000.hyps  55000.hyps  65000.hyps  75000.hyps  84000.hyps  92000.ckpt  latest.ckpt
102000.hyps  112000.hyps  16000.hyps   26000.hyps  36000.hyps  46000.hyps  56000.hyps  66000.hyps  76000.hyps  85000.hyps  92000.hyps  src_vocab.txt
103000.hyps  113000.hyps  17000.hyps   27000.hyps  37000.hyps  47000.hyps  57000.hyps  67000.hyps  77000.hyps  86000.hyps  93000.hyps  tensorboard
104000.hyps  114000.hyps  18000.hyps   28000.hyps  38000.hyps  48000.hyps  58000.hyps  68000.hyps  78000.hyps  87000.hyps  94000.hyps  train.log
105000.hyps  115000.hyps  19000.hyps   29000.hyps  39000.hyps  49000.hyps  59000.hyps  69000.hyps  79000.ckpt  88000.hyps  95000.hyps  trg_vocab.txt
106000.hyps  116000.hyps  20000.hyps   30000.hyps  40000.hyps  50000.hyps  60000.hyps  70000.hyps  79000.hyps  89000.ckpt  96000.hyps  validations.txt
107000.hyps  117000.hyps  2000.hyps    3000.hyps   4000.hyps   5000.hyps   6000.hyps   7000.hyps   80000.hyps  89000.hyps  97000.hyps
(joey) ye@:~/exp/joeynmt/models/wmt17_myrk_transformer$ 
```

validation.txt ဖိုင်ကို ဝင်ကြည့်ခဲ့...  

```
(joey) ye@:~/exp/joeynmt/models/wmt17_myrk_transformer$ cat validations.txt 
Steps: 1000	Loss: 16227.23047	PPL: 3.28919	bleu: 18.25736	LR: 0.00020000	*
Steps: 2000	Loss: 10198.37891	PPL: 2.11337	bleu: 40.00022	LR: 0.00020000	*
Steps: 3000	Loss: 7868.37305	PPL: 1.78127	bleu: 53.46309	LR: 0.00020000	*
Steps: 4000	Loss: 6856.99756	PPL: 1.65387	bleu: 57.86895	LR: 0.00020000	*
Steps: 5000	Loss: 6293.85547	PPL: 1.58693	bleu: 61.55079	LR: 0.00020000	*
Steps: 6000	Loss: 5650.06201	PPL: 1.51371	bleu: 65.60893	LR: 0.00020000	*
Steps: 7000	Loss: 5593.86328	PPL: 1.50748	bleu: 65.37050	LR: 0.00020000	*
Steps: 8000	Loss: 5299.16553	PPL: 1.47523	bleu: 67.03655	LR: 0.00020000	*
Steps: 9000	Loss: 4944.82275	PPL: 1.43737	bleu: 69.18242	LR: 0.00020000	*
Steps: 10000	Loss: 4827.76562	PPL: 1.42508	bleu: 71.80016	LR: 0.00020000	*
Steps: 11000	Loss: 4768.50781	PPL: 1.41890	bleu: 70.19907	LR: 0.00020000	*
Steps: 12000	Loss: 4492.50635	PPL: 1.39045	bleu: 72.83455	LR: 0.00020000	*
Steps: 13000	Loss: 4498.30225	PPL: 1.39104	bleu: 70.41476	LR: 0.00020000	
Steps: 14000	Loss: 4361.67920	PPL: 1.37717	bleu: 73.66593	LR: 0.00020000	*
Steps: 15000	Loss: 4350.81592	PPL: 1.37607	bleu: 72.62696	LR: 0.00020000	*
Steps: 16000	Loss: 4417.87305	PPL: 1.38286	bleu: 73.15372	LR: 0.00020000	
Steps: 17000	Loss: 4236.24023	PPL: 1.36455	bleu: 73.13667	LR: 0.00020000	*
Steps: 18000	Loss: 4128.94482	PPL: 1.35385	bleu: 74.12220	LR: 0.00020000	*
Steps: 19000	Loss: 4199.68311	PPL: 1.36090	bleu: 73.83125	LR: 0.00020000	
Steps: 20000	Loss: 4156.20020	PPL: 1.35656	bleu: 74.16584	LR: 0.00020000	
Steps: 21000	Loss: 4076.60205	PPL: 1.34866	bleu: 75.24400	LR: 0.00020000	*
Steps: 22000	Loss: 4038.23169	PPL: 1.34487	bleu: 73.74917	LR: 0.00020000	*
Steps: 23000	Loss: 4025.13794	PPL: 1.34358	bleu: 74.45245	LR: 0.00020000	*
Steps: 24000	Loss: 3992.31226	PPL: 1.34035	bleu: 74.91179	LR: 0.00020000	*
Steps: 25000	Loss: 4008.67554	PPL: 1.34196	bleu: 74.53116	LR: 0.00020000	
Steps: 26000	Loss: 3978.77075	PPL: 1.33901	bleu: 74.27662	LR: 0.00020000	*
Steps: 27000	Loss: 3995.29688	PPL: 1.34064	bleu: 74.38615	LR: 0.00020000	
Steps: 28000	Loss: 4069.66235	PPL: 1.34797	bleu: 73.43958	LR: 0.00020000	
Steps: 29000	Loss: 4024.77271	PPL: 1.34354	bleu: 74.20341	LR: 0.00020000	
Steps: 30000	Loss: 3850.61792	PPL: 1.32648	bleu: 75.68710	LR: 0.00020000	*
Steps: 31000	Loss: 3903.54346	PPL: 1.33164	bleu: 75.10386	LR: 0.00020000	
Steps: 32000	Loss: 3890.91382	PPL: 1.33041	bleu: 75.29977	LR: 0.00020000	
Steps: 33000	Loss: 3887.13013	PPL: 1.33004	bleu: 74.98858	LR: 0.00020000	
Steps: 34000	Loss: 3752.50879	PPL: 1.31697	bleu: 75.89772	LR: 0.00020000	*
Steps: 35000	Loss: 3862.02441	PPL: 1.32759	bleu: 74.76388	LR: 0.00020000	
Steps: 36000	Loss: 3889.14624	PPL: 1.33024	bleu: 75.52681	LR: 0.00020000	
Steps: 37000	Loss: 3919.73120	PPL: 1.33323	bleu: 75.13930	LR: 0.00020000	
Steps: 38000	Loss: 3820.85083	PPL: 1.32359	bleu: 76.25321	LR: 0.00020000	
Steps: 39000	Loss: 3860.60645	PPL: 1.32746	bleu: 74.94958	LR: 0.00020000	
Steps: 40000	Loss: 3855.87817	PPL: 1.32700	bleu: 75.64406	LR: 0.00020000	
Steps: 41000	Loss: 3758.04443	PPL: 1.31750	bleu: 75.51567	LR: 0.00020000	
Steps: 42000	Loss: 3839.28491	PPL: 1.32538	bleu: 75.43853	LR: 0.00020000	
Steps: 43000	Loss: 3843.43359	PPL: 1.32578	bleu: 76.24335	LR: 0.00014000	
Steps: 44000	Loss: 3526.22437	PPL: 1.29528	bleu: 77.60569	LR: 0.00014000	*
Steps: 45000	Loss: 3543.66992	PPL: 1.29694	bleu: 77.44380	LR: 0.00014000	
Steps: 46000	Loss: 3535.14575	PPL: 1.29613	bleu: 77.92938	LR: 0.00014000	
Steps: 47000	Loss: 3548.39624	PPL: 1.29739	bleu: 77.73633	LR: 0.00014000	
Steps: 48000	Loss: 3517.62012	PPL: 1.29447	bleu: 77.76691	LR: 0.00014000	*
Steps: 49000	Loss: 3448.23901	PPL: 1.28789	bleu: 78.49723	LR: 0.00014000	*
Steps: 50000	Loss: 3533.98511	PPL: 1.29602	bleu: 78.30917	LR: 0.00014000	
Steps: 51000	Loss: 3491.46533	PPL: 1.29198	bleu: 75.94287	LR: 0.00014000	
Steps: 52000	Loss: 3488.89111	PPL: 1.29174	bleu: 77.88675	LR: 0.00014000	
Steps: 53000	Loss: 3461.19507	PPL: 1.28912	bleu: 78.33570	LR: 0.00014000	
Steps: 54000	Loss: 3466.79736	PPL: 1.28965	bleu: 77.94780	LR: 0.00014000	
Steps: 55000	Loss: 3512.96265	PPL: 1.29402	bleu: 78.19317	LR: 0.00014000	
Steps: 56000	Loss: 3525.48462	PPL: 1.29521	bleu: 77.62910	LR: 0.00014000	
Steps: 57000	Loss: 3509.47217	PPL: 1.29369	bleu: 78.11619	LR: 0.00014000	
Steps: 58000	Loss: 3482.61646	PPL: 1.29115	bleu: 78.80497	LR: 0.00009800	
Steps: 59000	Loss: 3378.65747	PPL: 1.28133	bleu: 79.03452	LR: 0.00009800	*
Steps: 60000	Loss: 3369.04468	PPL: 1.28043	bleu: 79.23157	LR: 0.00009800	*
Steps: 61000	Loss: 3319.65869	PPL: 1.27580	bleu: 79.09594	LR: 0.00009800	*
Steps: 62000	Loss: 3380.00000	PPL: 1.28146	bleu: 78.83491	LR: 0.00009800	
Steps: 63000	Loss: 3380.91821	PPL: 1.28155	bleu: 78.34399	LR: 0.00009800	
Steps: 64000	Loss: 3337.79834	PPL: 1.27750	bleu: 79.08065	LR: 0.00009800	
Steps: 65000	Loss: 3350.18921	PPL: 1.27866	bleu: 79.15527	LR: 0.00009800	
Steps: 66000	Loss: 3311.55493	PPL: 1.27504	bleu: 78.62346	LR: 0.00009800	*
Steps: 67000	Loss: 3328.63940	PPL: 1.27664	bleu: 79.44776	LR: 0.00009800	
Steps: 68000	Loss: 3352.55615	PPL: 1.27888	bleu: 79.80149	LR: 0.00009800	
Steps: 69000	Loss: 3353.32666	PPL: 1.27896	bleu: 79.30337	LR: 0.00009800	
Steps: 70000	Loss: 3380.58911	PPL: 1.28152	bleu: 78.93046	LR: 0.00009800	
Steps: 71000	Loss: 3322.87085	PPL: 1.27610	bleu: 79.26434	LR: 0.00009800	
Steps: 72000	Loss: 3354.91211	PPL: 1.27910	bleu: 79.03954	LR: 0.00009800	
Steps: 73000	Loss: 3385.72656	PPL: 1.28200	bleu: 78.96060	LR: 0.00009800	
Steps: 74000	Loss: 3363.23682	PPL: 1.27989	bleu: 80.06282	LR: 0.00009800	
Steps: 75000	Loss: 3361.08521	PPL: 1.27968	bleu: 78.98610	LR: 0.00006860	
Steps: 76000	Loss: 3309.35742	PPL: 1.27484	bleu: 79.52576	LR: 0.00006860	*
Steps: 77000	Loss: 3333.19531	PPL: 1.27707	bleu: 79.72869	LR: 0.00006860	
Steps: 78000	Loss: 3299.64209	PPL: 1.27393	bleu: 80.11292	LR: 0.00006860	*
Steps: 79000	Loss: 3292.21606	PPL: 1.27323	bleu: 79.81080	LR: 0.00006860	*
Steps: 80000	Loss: 3341.37231	PPL: 1.27783	bleu: 79.43034	LR: 0.00006860	
Steps: 81000	Loss: 3321.38892	PPL: 1.27596	bleu: 80.24021	LR: 0.00006860	
Steps: 82000	Loss: 3321.88892	PPL: 1.27601	bleu: 80.42184	LR: 0.00006860	
Steps: 83000	Loss: 3342.02124	PPL: 1.27789	bleu: 79.64490	LR: 0.00006860	
Steps: 84000	Loss: 3327.28906	PPL: 1.27651	bleu: 79.73121	LR: 0.00006860	
Steps: 85000	Loss: 3345.78418	PPL: 1.27825	bleu: 79.86663	LR: 0.00006860	
Steps: 86000	Loss: 3340.71948	PPL: 1.27777	bleu: 79.69921	LR: 0.00006860	
Steps: 87000	Loss: 3320.47534	PPL: 1.27588	bleu: 80.00401	LR: 0.00006860	
Steps: 88000	Loss: 3317.85889	PPL: 1.27563	bleu: 80.04050	LR: 0.00004802	
Steps: 89000	Loss: 3286.95801	PPL: 1.27274	bleu: 80.34537	LR: 0.00004802	*
Steps: 90000	Loss: 3310.65527	PPL: 1.27496	bleu: 80.47454	LR: 0.00004802	
Steps: 91000	Loss: 3276.43335	PPL: 1.27176	bleu: 80.20973	LR: 0.00004802	*
Steps: 92000	Loss: 3272.47852	PPL: 1.27139	bleu: 79.79280	LR: 0.00004802	*
Steps: 93000	Loss: 3314.32104	PPL: 1.27530	bleu: 80.23317	LR: 0.00004802	
Steps: 94000	Loss: 3328.10815	PPL: 1.27659	bleu: 79.94806	LR: 0.00004802	
Steps: 95000	Loss: 3335.18237	PPL: 1.27725	bleu: 80.00039	LR: 0.00004802	
Steps: 96000	Loss: 3297.03540	PPL: 1.27368	bleu: 80.43140	LR: 0.00004802	
Steps: 97000	Loss: 3339.25488	PPL: 1.27764	bleu: 79.89044	LR: 0.00004802	
Steps: 98000	Loss: 3319.76001	PPL: 1.27581	bleu: 79.90487	LR: 0.00004802	
Steps: 99000	Loss: 3321.02368	PPL: 1.27593	bleu: 80.45157	LR: 0.00004802	
Steps: 100000	Loss: 3343.80371	PPL: 1.27806	bleu: 80.46689	LR: 0.00004802	
Steps: 101000	Loss: 3345.76514	PPL: 1.27825	bleu: 80.29121	LR: 0.00003361	
Steps: 102000	Loss: 3282.45605	PPL: 1.27232	bleu: 81.06587	LR: 0.00003361	
Steps: 103000	Loss: 3313.79785	PPL: 1.27525	bleu: 80.53232	LR: 0.00003361	
Steps: 104000	Loss: 3319.12573	PPL: 1.27575	bleu: 80.25901	LR: 0.00003361	
Steps: 105000	Loss: 3331.75684	PPL: 1.27693	bleu: 80.69237	LR: 0.00003361	
Steps: 106000	Loss: 3311.98999	PPL: 1.27508	bleu: 80.71984	LR: 0.00003361	
Steps: 107000	Loss: 3325.14233	PPL: 1.27631	bleu: 80.73467	LR: 0.00003361	
Steps: 108000	Loss: 3338.11963	PPL: 1.27753	bleu: 80.37323	LR: 0.00003361	
Steps: 109000	Loss: 3338.30225	PPL: 1.27755	bleu: 80.42921	LR: 0.00003361	
Steps: 110000	Loss: 3328.72412	PPL: 1.27665	bleu: 80.50599	LR: 0.00002353	
Steps: 111000	Loss: 3314.75146	PPL: 1.27534	bleu: 80.86648	LR: 0.00002353	
Steps: 112000	Loss: 3321.08887	PPL: 1.27593	bleu: 80.94222	LR: 0.00002353	
Steps: 113000	Loss: 3308.48047	PPL: 1.27475	bleu: 80.75950	LR: 0.00002353	
Steps: 114000	Loss: 3320.16455	PPL: 1.27585	bleu: 80.89520	LR: 0.00002353	
Steps: 115000	Loss: 3324.58716	PPL: 1.27626	bleu: 80.86534	LR: 0.00002353	
Steps: 116000	Loss: 3323.23877	PPL: 1.27613	bleu: 81.13362	LR: 0.00002353	
Steps: 117000	Loss: 3317.83887	PPL: 1.27563	bleu: 81.04013	LR: 0.00002353	
Steps: 118000	Loss: 3304.48877	PPL: 1.27438	bleu: 81.24831	LR: 0.00002353	
(joey) ye@:~/exp/joeynmt/models/wmt17_myrk_transformer$
```

ဒီမော်ဒယ်က baseline အဖြစ် ထားလို့ ရလို့ backup ကူးခဲ့...  

```
(joey) ye@:~/exp/joeynmt/models$ mv wmt17_myrk_transformer/ wmt17_myrk_transformer1
```

## Training Transformer Baseline for Rakhine-Myanmar

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/transformer_wmt17_rkmy.yaml 
2022-03-02 01:03:23,638 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-03-02 01:03:23,663 - INFO - joeynmt.data - Loading training data...
2022-03-02 01:03:26,666 - INFO - joeynmt.data - Building vocabulary...
2022-03-02 01:03:26,745 - INFO - joeynmt.data - Loading dev data...
2022-03-02 01:03:26,778 - INFO - joeynmt.data - Loading test data...
2022-03-02 01:03:26,823 - INFO - joeynmt.data - Data loaded.
2022-03-02 01:03:26,823 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-03-02 01:03:27,395 - INFO - joeynmt.model - Enc-dec model built.
2022-03-02 01:03:27.655536: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-03-02 01:03:29,172 - INFO - joeynmt.training - Total params: 46633472
2022-03-02 01:03:34,370 - INFO - joeynmt.helpers -                           cfg.name : transformer_rkmy
2022-03-02 01:03:34,370 - INFO - joeynmt.helpers -                       cfg.data.src : rk
2022-03-02 01:03:34,370 - INFO - joeynmt.helpers -                       cfg.data.trg : my
2022-03-02 01:03:34,370 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 100
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-03-02 01:03:34,371 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -         cfg.training.normalization : tokens
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -            cfg.training.adam_betas : [0.9, 0.999]
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -              cfg.training.patience : 8
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.7
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -                  cfg.training.loss : crossentropy
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0002
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 1e-08
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-03-02 01:03:34,372 - INFO - joeynmt.helpers -       cfg.training.label_smoothing : 0.1
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -            cfg.training.batch_size : 128
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -            cfg.training.batch_type : token
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -       cfg.training.eval_batch_size : 128
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -       cfg.training.eval_batch_type : token
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -      cfg.training.batch_multiplier : 1
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : ppl
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -                cfg.training.epochs : 100
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt17_rkmy_transformer1
2022-03-02 01:03:34,373 - INFO - joeynmt.helpers -             cfg.training.overwrite : False
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2, 3]
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 5
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -                cfg.model.init_gain : 1.0
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : xavier
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -          cfg.model.embed_init_gain : 1.0
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -          cfg.model.tied_embeddings : False
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -             cfg.model.tied_softmax : False
2022-03-02 01:03:34,374 - INFO - joeynmt.helpers -             cfg.model.encoder.type : transformer
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 6
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -        cfg.model.encoder.num_heads : 8
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 512
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : True
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.dropout : 0.0
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 512
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -          cfg.model.encoder.ff_size : 2048
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -             cfg.model.decoder.type : transformer
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 6
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers -        cfg.model.decoder.num_heads : 8
2022-03-02 01:03:34,375 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 512
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : True
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.dropout : 0.0
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 512
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers -          cfg.model.decoder.ff_size : 2048
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - Data set sizes: 
	train 15561,
	valid 1000,
	test 1811
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
	[TRG] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-03-02 01:03:34,376 - INFO - joeynmt.helpers - Number of Src words (types): 1695
2022-03-02 01:03:34,377 - INFO - joeynmt.helpers - Number of Trg words (types): 1587
2022-03-02 01:03:34,377 - INFO - joeynmt.training - Model(
	encoder=TransformerEncoder(num_layers=6, num_heads=8),
	decoder=TransformerDecoder(num_layers=6, num_heads=8),
	src_embed=Embeddings(embedding_dim=512, vocab_size=1695),
	trg_embed=Embeddings(embedding_dim=512, vocab_size=1587))
2022-03-02 01:03:34,379 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 64
	total batch size (w. parallel & accumulation): 128
2022-03-02 01:03:34,380 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 447, in train_and_validate
    batch_loss += self._train_step(batch)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 569, in _train_step
    norm_batch_loss.backward()
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_tensor.py", line 307, in backward
    torch.autograd.backward(self, gradient, retain_graph, create_graph, inputs=inputs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/autograd/__init__.py", line 154, in backward
    Variable._execution_engine.run_backward(
  File "/home/ye/.local/lib/python3.8/site-packages/torch/autograd/function.py", line 199, in apply
    return user_fn(self, *args)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py", line 34, in backward
    return (None,) + ReduceAddCoalesced.apply(ctx.input_device, ctx.num_inputs, *grad_outputs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py", line 45, in forward
    return comm.reduce_add_coalesced(grads_, destination)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/comm.py", line 142, in reduce_add_coalesced
    flat_tensors = [_flatten_dense_tensors(chunk) for chunk in chunks]  # (num_gpus,)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/comm.py", line 142, in <listcomp>
    flat_tensors = [_flatten_dense_tensors(chunk) for chunk in chunks]  # (num_gpus,)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_utils.py", line 265, in _flatten_dense_tensors
    return torch._C._nn.flatten_dense_tensors(tensors)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 1001.35 MiB already allocated; 85.25 MiB free; 1.03 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF

real	0m16.211s
user	0m7.081s
sys	0m4.030s

```

Memory error တက်တယ်။ အဲဒါကြောင့် စက်ကို restart လုပ်ပြီး ပြန် run ကြည့်ခဲ့...  
