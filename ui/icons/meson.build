foreach s: [16, 24, 32, 48, 64, 128, 256, 512]
  s = '@0@x@0@'.format(s.to_string())
  install_data('lotus_@0@.png'.format(s),
               rename: 'lotus.png',
               install_dir: lotus_icondir / 'hicolor' / s / 'apps')
endforeach

install_data('lotus.svg',
             install_dir: lotus_icondir / 'hicolor' / 'scalable' / 'apps')
