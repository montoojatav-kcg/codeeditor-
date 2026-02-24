<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CEWCMM — by MONTOO</title>
<style>
/* ══════════════════════════════════════════════════
   CEWCMM — Full VS Code Clone · by MONTOO
   ══════════════════════════════════════════════════ */
@import url('https://fonts.googleapis.com/css2?family=Consolas&display=swap');

*{margin:0;padding:0;box-sizing:border-box;user-select:none;}
textarea,input{user-select:text;}

:root{
  --titlebar:#3c3c3c;
  --menubar:#3c3c3c;
  --actbar:#333333;
  --sidebar:#252526;
  --sidebar-border:#1e1e1e;
  --sidebar-hover:#2a2d2e;
  --sidebar-active:#094771;
  --sidebar-text:#cccccc;
  --sidebar-muted:#858585;
  --editor-bg:#1e1e1e;
  --editor-fg:#d4d4d4;
  --editor-line:#2a2d2e;
  --editor-sel:#264f78;
  --editor-word:#575757;
  --tab-bar:#252526;
  --tab-active:#1e1e1e;
  --tab-inactive:#2d2d2d;
  --tab-border:#007acc;
  --panel-bg:#1e1e1e;
  --panel-header:#252526;
  --statusbar:#007acc;
  --statusbar-fg:#fff;
  --line-num:#858585;
  --line-num-active:#c6c6c6;
  --minimap-bg:#252526;
  --scrollbar:#424242;
  --border:#1e1e1e;
  --input-bg:#3c3c3c;
  --input-border:#555;
  --btn-bg:#0e639c;
  --btn-hover:#1177bb;
  --dropdown-bg:#252526;
  --dropdown-border:#454545;
  --hover-bg:rgba(255,255,255,0.07);
  --focus:#007acc;

  /* Syntax — Dark+ */
  --s-kw:#569cd6;
  --s-str:#ce9178;
  --s-cmt:#6a9955;
  --s-num:#b5cea8;
  --s-fn:#dcdcaa;
  --s-cls:#4ec9b0;
  --s-prop:#9cdcfe;
  --s-op:#d4d4d4;
  --s-tag:#569cd6;
  --s-attr:#9cdcfe;
  --s-val:#ce9178;
  --s-bool:#569cd6;
  --s-rx:#d16969;
  --s-dec:#4fc1ff;
  --s-type:#4ec9b0;

  --font-size:13px;
  --line-height:19px;
  --tab-size:4;
}

/* Light theme */
body.light{
  --titlebar:#dddddd;
  --menubar:#dddddd;
  --actbar:#2c2c2c;
  --sidebar:#f3f3f3;
  --sidebar-border:#e5e5e5;
  --sidebar-hover:#e8e8e8;
  --sidebar-active:#cce5ff;
  --sidebar-text:#333333;
  --sidebar-muted:#888888;
  --editor-bg:#ffffff;
  --editor-fg:#000000;
  --editor-line:#f5f5f5;
  --editor-sel:#add6ff;
  --tab-bar:#ececec;
  --tab-active:#ffffff;
  --tab-inactive:#ececec;
  --tab-border:#005fb8;
  --panel-bg:#f3f3f3;
  --panel-header:#ececec;
  --line-num:#999999;
  --line-num-active:#333333;
  --minimap-bg:#f3f3f3;
  --scrollbar:#c1c1c1;
  --border:#e5e5e5;
  --input-bg:#ffffff;
  --input-border:#ccc;
  --dropdown-bg:#ffffff;
  --dropdown-border:#ccc;
  --hover-bg:rgba(0,0,0,0.06);
  --s-kw:#0000ff;
  --s-str:#a31515;
  --s-cmt:#008000;
  --s-num:#098658;
  --s-fn:#795e26;
  --s-cls:#267f99;
  --s-prop:#001080;
  --s-tag:#800000;
  --s-attr:#e50000;
  --s-val:#a31515;
  --s-bool:#0000ff;
}

html,body{height:100%;overflow:hidden;font-family:'Segoe UI',system-ui,sans-serif;font-size:13px;}
body{display:flex;flex-direction:column;background:var(--editor-bg);color:var(--editor-fg);}

/* ── TITLE BAR ── */
.titlebar{
  height:30px;background:var(--titlebar);
  display:flex;align-items:center;
  flex-shrink:0;position:relative;
  border-bottom:1px solid rgba(0,0,0,0.3);
  -webkit-app-region:drag;
}
.tdots{display:flex;gap:6px;padding:0 12px;-webkit-app-region:no-drag;}
.tdot{width:12px;height:12px;border-radius:50%;cursor:pointer;transition:filter .15s;}
.tdot:hover{filter:brightness(1.3);}
.tdot-r{background:#ff5f57;}
.tdot-y{background:#ffbd2e;}
.tdot-g{background:#28c840;}
.tmenus{display:flex;-webkit-app-region:no-drag;}
.tmenu{
  font-size:12px;color:rgba(255,255,255,0.75);
  padding:0 8px;height:30px;line-height:30px;
  cursor:pointer;white-space:nowrap;transition:background .1s;
}
body.light .tmenu{color:rgba(0,0,0,0.7);}
.tmenu:hover,.tmenu.open{background:var(--hover-bg);}
.ttitle{
  position:absolute;left:50%;transform:translateX(-50%);
  font-size:12px;color:rgba(255,255,255,0.7);pointer-events:none;white-space:nowrap;
}
body.light .ttitle{color:rgba(0,0,0,0.6);}
.tcontrols{margin-left:auto;display:flex;-webkit-app-region:no-drag;}
.tctrl{
  width:46px;height:30px;display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:rgba(255,255,255,0.7);font-size:12px;transition:background .1s;
}
body.light .tctrl{color:rgba(0,0,0,0.7);}
.tctrl:hover{background:rgba(255,255,255,0.1);}
.tctrl.cl:hover{background:#e81123;color:#fff;}

/* ── DROPDOWN MENUS ── */
.dropdown{
  position:fixed;background:var(--dropdown-bg);
  border:1px solid var(--dropdown-border);
  border-radius:4px;min-width:220px;
  padding:4px 0;z-index:9999;
  box-shadow:0 8px 24px rgba(0,0,0,0.4);
  display:none;
}
.dropdown.show{display:block;}
.dd-item{
  padding:5px 24px 5px 12px;font-size:12px;
  cursor:pointer;color:var(--sidebar-text);
  display:flex;align-items:center;justify-content:space-between;
  white-space:nowrap;transition:background .07s;
}
.dd-item:hover{background:var(--sidebar-active);color:#fff;}
.dd-item.disabled{color:var(--sidebar-muted);cursor:default;}
.dd-item.disabled:hover{background:none;color:var(--sidebar-muted);}
.dd-sep{height:1px;background:var(--dropdown-border);margin:4px 0;}
.dd-key{font-size:11px;color:var(--sidebar-muted);margin-left:16px;}
.dd-item:hover .dd-key{color:rgba(255,255,255,0.6);}
.dd-arrow{color:var(--sidebar-muted);margin-left:8px;}

/* ── APP BODY ── */
.appbody{display:flex;flex:1;overflow:hidden;}

/* ── ACTIVITY BAR ── */
.actbar{
  width:48px;background:var(--actbar);
  display:flex;flex-direction:column;align-items:center;
  padding-top:0;flex-shrink:0;
  border-right:1px solid var(--border);
}
.ab-item{
  width:48px;height:48px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;position:relative;
  color:rgba(255,255,255,0.4);transition:color .12s;
}
.ab-item:hover{color:rgba(255,255,255,0.9);}
.ab-item.active{color:#ffffff;}
.ab-item.active::before{
  content:'';position:absolute;left:0;top:10px;bottom:10px;
  width:2px;background:#fff;border-radius:0 2px 2px 0;
}
.ab-icon{font-size:20px;line-height:1;}
.ab-badge{
  position:absolute;top:7px;right:7px;
  background:#007acc;color:#fff;
  font-size:9px;font-weight:700;
  min-width:14px;height:14px;
  border-radius:7px;padding:0 3px;
  display:flex;align-items:center;justify-content:center;
}
.ab-bottom{margin-top:auto;margin-bottom:4px;}
.ab-tooltip{
  position:absolute;left:52px;
  background:rgba(80,80,80,0.95);color:#fff;
  font-size:12px;padding:4px 8px;border-radius:3px;
  white-space:nowrap;pointer-events:none;display:none;z-index:100;
}
.ab-item:hover .ab-tooltip{display:block;}

/* ── SIDEBAR ── */
.sidebar{
  width:260px;background:var(--sidebar);
  display:flex;flex-direction:column;
  border-right:1px solid var(--sidebar-border);
  flex-shrink:0;overflow:hidden;transition:width .15s;
}
.sidebar.collapsed{width:0;}
.sb-title{
  height:35px;display:flex;align-items:center;justify-content:space-between;
  padding:0 12px;font-size:11px;font-weight:600;
  letter-spacing:1.2px;text-transform:uppercase;
  color:var(--sidebar-text);flex-shrink:0;
}
.sb-actions{display:flex;gap:2px;}
.sb-btn{
  width:22px;height:22px;border-radius:4px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:14px;
  transition:all .1s;
}
.sb-btn:hover{background:var(--hover-bg);color:var(--sidebar-text);}

/* File tree */
.file-tree{flex:1;overflow-y:auto;overflow-x:hidden;}
.file-tree::-webkit-scrollbar{width:6px;}
.file-tree::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}
.tree-row{
  height:22px;display:flex;align-items:center;
  cursor:pointer;padding-right:8px;font-size:13px;
  color:var(--sidebar-text);position:relative;transition:background .05s;
}
.tree-row:hover{background:var(--sidebar-hover);}
.tree-row.selected{background:var(--sidebar-active);}
.tree-row.selected::before{content:'';position:absolute;left:0;top:0;bottom:0;width:1px;background:#007acc;}
.tree-row.cut{opacity:0.5;}
.tree-indent{flex-shrink:0;}
.tree-arrow{width:16px;flex-shrink:0;font-size:9px;color:var(--sidebar-muted);display:flex;align-items:center;justify-content:center;}
.tree-icon{width:18px;flex-shrink:0;font-size:14px;}
.tree-name{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:13px;}
.tree-row.renaming .tree-name{display:none;}
.rename-input{
  flex:1;background:var(--input-bg);border:1px solid #007acc;
  color:var(--sidebar-text);font-size:13px;padding:0 4px;outline:none;height:18px;
}

/* ── SEARCH SIDEBAR ── */
.search-sb{padding:8px;display:flex;flex-direction:column;gap:6px;flex:1;overflow:hidden;}
.search-row{display:flex;gap:4px;align-items:center;}
.sb-input{
  flex:1;background:var(--input-bg);border:1px solid var(--input-border);
  color:var(--sidebar-text);font-size:12px;padding:4px 8px;outline:none;border-radius:2px;
  font-family:inherit;
}
.sb-input:focus{border-color:#007acc;}
.sb-toggle{
  width:24px;height:24px;border-radius:3px;background:none;border:1px solid transparent;
  color:var(--sidebar-muted);cursor:pointer;font-size:12px;display:flex;align-items:center;justify-content:center;
  transition:all .1s;
}
.sb-toggle:hover{background:var(--hover-bg);color:var(--sidebar-text);}
.sb-toggle.on{background:var(--sidebar-active);color:#fff;border-color:#007acc;}
.search-results{flex:1;overflow-y:auto;font-size:12px;}
.search-results::-webkit-scrollbar{width:4px;}
.search-results::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.sr-file{padding:4px 8px;color:var(--sidebar-text);font-weight:600;cursor:pointer;display:flex;align-items:center;gap:4px;}
.sr-file:hover{background:var(--sidebar-hover);}
.sr-match{
  padding:2px 8px 2px 28px;color:var(--sidebar-muted);cursor:pointer;
  display:flex;gap:4px;align-items:flex-start;
}
.sr-match:hover{background:var(--sidebar-hover);color:var(--sidebar-text);}
.sr-line-num{color:#858585;flex-shrink:0;min-width:28px;text-align:right;}
.sr-text{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.sr-hl{background:rgba(255,200,0,0.3);border-radius:2px;}
.sr-count{font-size:11px;color:var(--sidebar-muted);padding:4px 8px;}

/* ── GIT SIDEBAR ── */
.git-sb{padding:8px;display:flex;flex-direction:column;gap:8px;flex:1;overflow-y:auto;}
.git-commit-area{display:flex;flex-direction:column;gap:6px;}
.git-msg{
  width:100%;background:var(--input-bg);border:1px solid var(--input-border);
  color:var(--sidebar-text);font-size:12px;padding:6px 8px;outline:none;border-radius:2px;
  resize:vertical;min-height:60px;font-family:inherit;
}
.git-msg:focus{border-color:#007acc;}
.git-commit-btn{
  background:var(--btn-bg);color:#fff;border:none;padding:5px 10px;
  border-radius:2px;cursor:pointer;font-size:12px;font-weight:600;
  transition:background .1s;
}
.git-commit-btn:hover{background:var(--btn-hover);}
.git-section{font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--sidebar-muted);padding:4px 0;}
.git-file{
  display:flex;align-items:center;gap:6px;padding:3px 4px;
  border-radius:3px;cursor:pointer;transition:background .07s;
  color:var(--sidebar-text);font-size:12px;
}
.git-file:hover{background:var(--sidebar-hover);}
.git-status{width:14px;font-weight:700;font-size:11px;flex-shrink:0;}
.git-status.M{color:#cca700;}
.git-status.U{color:#89d185;}
.git-status.D{color:#f48771;}
.git-status.A{color:#89d185;}
.git-actions{margin-left:auto;display:flex;gap:2px;opacity:0;transition:opacity .1s;}
.git-file:hover .git-actions{opacity:1;}
.git-act-btn{
  width:18px;height:18px;border-radius:2px;background:none;border:none;
  color:var(--sidebar-muted);cursor:pointer;font-size:11px;display:flex;align-items:center;justify-content:center;
}
.git-act-btn:hover{background:var(--hover-bg);color:var(--sidebar-text);}

/* ── EXTENSIONS SIDEBAR ── */
.ext-list{flex:1;overflow-y:auto;}
.ext-item{
  padding:10px 12px;display:flex;gap:10px;cursor:pointer;
  border-bottom:1px solid var(--border);transition:background .07s;
}
.ext-item:hover{background:var(--sidebar-hover);}
.ext-icon{width:40px;height:40px;border-radius:6px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:22px;}
.ext-info{flex:1;min-width:0;}
.ext-name{font-size:13px;font-weight:600;color:var(--sidebar-text);}
.ext-desc{font-size:11px;color:var(--sidebar-muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:2px;}
.ext-meta{display:flex;gap:6px;margin-top:4px;align-items:center;}
.ext-pub{font-size:11px;color:var(--sidebar-muted);}
.ext-stars{font-size:11px;color:#cca700;}
.ext-install-btn{
  padding:3px 10px;border-radius:2px;background:var(--btn-bg);color:#fff;
  border:none;cursor:pointer;font-size:11px;font-weight:600;white-space:nowrap;
  transition:background .1s;
}
.ext-install-btn:hover{background:var(--btn-hover);}
.ext-install-btn.installed{background:none;border:1px solid var(--input-border);color:var(--sidebar-text);}

/* ── EDITOR ZONE ── */
.edzone{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0;}

/* ── TABS ── */
.tabs-bar{
  height:35px;background:var(--tab-bar);
  display:flex;align-items:flex-end;
  border-bottom:1px solid var(--border);
  overflow-x:auto;flex-shrink:0;
}
.tabs-bar::-webkit-scrollbar{height:2px;}
.tabs-bar::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.tab{
  height:35px;display:flex;align-items:center;gap:6px;
  padding:0 10px;cursor:pointer;border-right:1px solid var(--border);
  white-space:nowrap;flex-shrink:0;position:relative;
  background:var(--tab-inactive);color:rgba(255,255,255,0.45);
  transition:color .1s,background .1s;font-size:13px;
  min-width:80px;max-width:180px;
}
body.light .tab{color:rgba(0,0,0,0.4);}
.tab.active{background:var(--tab-active);color:var(--editor-fg);}
.tab.active::after{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:var(--tab-border);}
.tab:hover:not(.active){background:var(--sidebar-hover);color:var(--editor-fg);}
.tab-icon{font-size:13px;flex-shrink:0;}
.tab-name{flex:1;overflow:hidden;text-overflow:ellipsis;font-size:13px;}
.tab-dirty{width:8px;height:8px;border-radius:50%;background:rgba(255,255,255,0.5);flex-shrink:0;}
.tab.active .tab-dirty{background:var(--editor-fg);}
.tab-x{
  width:18px;height:18px;border-radius:3px;flex-shrink:0;
  display:flex;align-items:center;justify-content:center;
  font-size:14px;color:var(--sidebar-muted);transition:all .1s;
}
.tab:hover .tab-x{color:var(--editor-fg);}
.tab-x:hover{background:rgba(255,255,255,0.15)!important;}
.tab-add{
  width:30px;height:35px;display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:18px;flex-shrink:0;
}
.tab-add:hover{color:var(--editor-fg);}

/* ── BREADCRUMB ── */
.breadcrumb{
  height:22px;background:var(--editor-bg);
  border-bottom:1px solid var(--border);
  display:flex;align-items:center;padding:0 14px;gap:2px;
  font-size:12px;color:var(--sidebar-muted);flex-shrink:0;overflow:hidden;
}
.bc-item{cursor:pointer;padding:0 2px;border-radius:2px;transition:background .1s;}
.bc-item:hover{background:var(--hover-bg);color:var(--editor-fg);}
.bc-sep{color:rgba(255,255,255,0.2);}
body.light .bc-sep{color:rgba(0,0,0,0.2);}
.bc-last{color:var(--editor-fg);}

/* ── EDITOR SPLIT ── */
.split-v{display:flex;flex-direction:column;flex:1;overflow:hidden;}
.editor-group{flex:1;display:flex;overflow:hidden;}

/* ── EDITOR PANE ── */
.editor-pane{flex:1;display:flex;overflow:hidden;position:relative;}
.gutter{
  width:60px;background:var(--editor-bg);flex-shrink:0;
  overflow:hidden;border-right:1px solid transparent;
  display:flex;flex-direction:column;
}
.gutter-nums{
  padding:0 10px 0 4px;
  font-family:'Consolas','Courier New',monospace;
  font-size:var(--font-size);line-height:var(--line-height);
  color:var(--line-num);text-align:right;white-space:pre;
  padding-top:10px;
}
.code-wrap{flex:1;overflow:auto;position:relative;}
.code-wrap::-webkit-scrollbar{width:10px;height:10px;}
.code-wrap::-webkit-scrollbar-track{background:var(--editor-bg);}
.code-wrap::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}
.code-wrap::-webkit-scrollbar-corner{background:var(--editor-bg);}
.code-editor{
  min-height:100%;min-width:100%;width:max-content;
  padding:10px 0;font-family:'Consolas','Courier New',monospace;
  font-size:var(--font-size);line-height:var(--line-height);
  color:var(--editor-fg);background:transparent;
  border:none;resize:none;outline:none;tab-size:4;
  caret-color:#aeafad;white-space:pre;overflow:hidden;
}
.code-editor.wrap{white-space:pre-wrap;width:100%;}

/* ── MINIMAP ── */
.minimap{
  width:80px;background:var(--minimap-bg);
  border-left:1px solid var(--border);flex-shrink:0;
  overflow:hidden;position:relative;cursor:pointer;
}
.mm-viewport{
  position:absolute;left:0;right:0;
  background:rgba(255,255,255,0.08);
  pointer-events:none;min-height:20px;
}
.mm-code{
  padding:4px;font-size:2px;line-height:3px;
  font-family:monospace;white-space:pre;
  overflow:hidden;pointer-events:none;
  color:var(--editor-fg);opacity:0.4;
  transform-origin:top left;
}

/* ── PANEL ── */
.panel{
  background:var(--panel-bg);flex-shrink:0;
  border-top:1px solid var(--border);
  display:flex;flex-direction:column;
  min-height:28px;
}
.panel.closed{height:28px!important;}
.panel-header{
  height:28px;background:var(--panel-header);
  display:flex;align-items:center;
  border-bottom:1px solid var(--border);
  flex-shrink:0;
}
.panel-tabs-wrap{display:flex;align-items:flex-end;flex:1;padding-left:8px;height:100%;}
.ptab{
  height:28px;display:flex;align-items:center;
  padding:0 12px;font-size:11px;font-weight:600;
  letter-spacing:0.5px;text-transform:uppercase;
  color:var(--sidebar-muted);cursor:pointer;
  border-bottom:1px solid transparent;transition:all .1s;
}
.ptab:hover{color:var(--editor-fg);}
.ptab.active{color:var(--editor-fg);border-bottom-color:var(--editor-fg);}
.panel-acts{display:flex;align-items:center;gap:2px;padding:0 8px;margin-left:auto;}
.panel-act{
  width:22px;height:22px;border-radius:4px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:13px;transition:all .1s;
}
.panel-act:hover{background:var(--hover-bg);color:var(--editor-fg);}
.panel-body{flex:1;overflow:hidden;display:flex;flex-direction:column;}
.panel-content{
  flex:1;overflow-y:auto;overflow-x:auto;
  padding:4px 0;
}
.panel-content::-webkit-scrollbar{width:6px;height:6px;}
.panel-content::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}

/* Terminal */
.terminal{
  flex:1;overflow-y:auto;overflow-x:hidden;
  padding:4px 12px;
  font-family:'Consolas','Courier New',monospace;
  font-size:13px;line-height:1.5;color:#cccccc;
}
.terminal::-webkit-scrollbar{width:6px;}
.terminal::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.term-line{white-space:pre-wrap;word-break:break-all;margin:1px 0;}
.term-prompt{color:#4ec9b0;}
.term-ok{color:#89d185;}
.term-err{color:#f48771;}
.term-warn{color:#cca700;}
.term-info{color:#569cd6;}
.term-dim{color:#858585;}
.term-bold{font-weight:700;}
.term-input-row{display:flex;align-items:center;gap:4px;padding:2px 0;}
.term-input{
  flex:1;background:transparent;border:none;outline:none;
  color:#cccccc;font-family:'Consolas','Courier New',monospace;
  font-size:13px;caret-color:#aeafad;
}<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CEWCMM — by MONTOO</title>
<style>
/* ══════════════════════════════════════════════════
   CEWCMM — Full VS Code Clone · by MONTOO
   ══════════════════════════════════════════════════ */
@import url('https://fonts.googleapis.com/css2?family=Consolas&display=swap');

*{margin:0;padding:0;box-sizing:border-box;user-select:none;}
textarea,input{user-select:text;}

:root{
  --titlebar:#3c3c3c;
  --menubar:#3c3c3c;
  --actbar:#333333;
  --sidebar:#252526;
  --sidebar-border:#1e1e1e;
  --sidebar-hover:#2a2d2e;
  --sidebar-active:#094771;
  --sidebar-text:#cccccc;
  --sidebar-muted:#858585;
  --editor-bg:#1e1e1e;
  --editor-fg:#d4d4d4;
  --editor-line:#2a2d2e;
  --editor-sel:#264f78;
  --editor-word:#575757;
  --tab-bar:#252526;
  --tab-active:#1e1e1e;
  --tab-inactive:#2d2d2d;
  --tab-border:#007acc;
  --panel-bg:#1e1e1e;
  --panel-header:#252526;
  --statusbar:#007acc;
  --statusbar-fg:#fff;
  --line-num:#858585;
  --line-num-active:#c6c6c6;
  --minimap-bg:#252526;
  --scrollbar:#424242;
  --border:#1e1e1e;
  --input-bg:#3c3c3c;
  --input-border:#555;
  --btn-bg:#0e639c;
  --btn-hover:#1177bb;
  --dropdown-bg:#252526;
  --dropdown-border:#454545;
  --hover-bg:rgba(255,255,255,0.07);
  --focus:#007acc;

  /* Syntax — Dark+ */
  --s-kw:#569cd6;
  --s-str:#ce9178;
  --s-cmt:#6a9955;
  --s-num:#b5cea8;
  --s-fn:#dcdcaa;
  --s-cls:#4ec9b0;
  --s-prop:#9cdcfe;
  --s-op:#d4d4d4;
  --s-tag:#569cd6;
  --s-attr:#9cdcfe;
  --s-val:#ce9178;
  --s-bool:#569cd6;
  --s-rx:#d16969;
  --s-dec:#4fc1ff;
  --s-type:#4ec9b0;

  --font-size:13px;
  --line-height:19px;
  --tab-size:4;
}

/* Light theme */
body.light{
  --titlebar:#dddddd;
  --menubar:#dddddd;
  --actbar:#2c2c2c;
  --sidebar:#f3f3f3;
  --sidebar-border:#e5e5e5;
  --sidebar-hover:#e8e8e8;
  --sidebar-active:#cce5ff;
  --sidebar-text:#333333;
  --sidebar-muted:#888888;
  --editor-bg:#ffffff;
  --editor-fg:#000000;
  --editor-line:#f5f5f5;
  --editor-sel:#add6ff;
  --tab-bar:#ececec;
  --tab-active:#ffffff;
  --tab-inactive:#ececec;
  --tab-border:#005fb8;
  --panel-bg:#f3f3f3;
  --panel-header:#ececec;
  --line-num:#999999;
  --line-num-active:#333333;
  --minimap-bg:#f3f3f3;
  --scrollbar:#c1c1c1;
  --border:#e5e5e5;
  --input-bg:#ffffff;
  --input-border:#ccc;
  --dropdown-bg:#ffffff;
  --dropdown-border:#ccc;
  --hover-bg:rgba(0,0,0,0.06);
  --s-kw:#0000ff;
  --s-str:#a31515;
  --s-cmt:#008000;
  --s-num:#098658;
  --s-fn:#795e26;
  --s-cls:#267f99;
  --s-prop:#001080;
  --s-tag:#800000;
  --s-attr:#e50000;
  --s-val:#a31515;
  --s-bool:#0000ff;
}

html,body{height:100%;overflow:hidden;font-family:'Segoe UI',system-ui,sans-serif;font-size:13px;}
body{display:flex;flex-direction:column;background:var(--editor-bg);color:var(--editor-fg);}

/* ── TITLE BAR ── */
.titlebar{
  height:30px;background:var(--titlebar);
  display:flex;align-items:center;
  flex-shrink:0;position:relative;
  border-bottom:1px solid rgba(0,0,0,0.3);
  -webkit-app-region:drag;
}
.tdots{display:flex;gap:6px;padding:0 12px;-webkit-app-region:no-drag;}
.tdot{width:12px;height:12px;border-radius:50%;cursor:pointer;transition:filter .15s;}
.tdot:hover{filter:brightness(1.3);}
.tdot-r{background:#ff5f57;}
.tdot-y{background:#ffbd2e;}
.tdot-g{background:#28c840;}
.tmenus{display:flex;-webkit-app-region:no-drag;}
.tmenu{
  font-size:12px;color:rgba(255,255,255,0.75);
  padding:0 8px;height:30px;line-height:30px;
  cursor:pointer;white-space:nowrap;transition:background .1s;
}
body.light .tmenu{color:rgba(0,0,0,0.7);}
.tmenu:hover,.tmenu.open{background:var(--hover-bg);}
.ttitle{
  position:absolute;left:50%;transform:translateX(-50%);
  font-size:12px;color:rgba(255,255,255,0.7);pointer-events:none;white-space:nowrap;
}
body.light .ttitle{color:rgba(0,0,0,0.6);}
.tcontrols{margin-left:auto;display:flex;-webkit-app-region:no-drag;}
.tctrl{
  width:46px;height:30px;display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:rgba(255,255,255,0.7);font-size:12px;transition:background .1s;
}
body.light .tctrl{color:rgba(0,0,0,0.7);}
.tctrl:hover{background:rgba(255,255,255,0.1);}
.tctrl.cl:hover{background:#e81123;color:#fff;}

/* ── DROPDOWN MENUS ── */
.dropdown{
  position:fixed;background:var(--dropdown-bg);
  border:1px solid var(--dropdown-border);
  border-radius:4px;min-width:220px;
  padding:4px 0;z-index:9999;
  box-shadow:0 8px 24px rgba(0,0,0,0.4);
  display:none;
}
.dropdown.show{display:block;}
.dd-item{
  padding:5px 24px 5px 12px;font-size:12px;
  cursor:pointer;color:var(--sidebar-text);
  display:flex;align-items:center;justify-content:space-between;
  white-space:nowrap;transition:background .07s;
}
.dd-item:hover{background:var(--sidebar-active);color:#fff;}
.dd-item.disabled{color:var(--sidebar-muted);cursor:default;}
.dd-item.disabled:hover{background:none;color:var(--sidebar-muted);}
.dd-sep{height:1px;background:var(--dropdown-border);margin:4px 0;}
.dd-key{font-size:11px;color:var(--sidebar-muted);margin-left:16px;}
.dd-item:hover .dd-key{color:rgba(255,255,255,0.6);}
.dd-arrow{color:var(--sidebar-muted);margin-left:8px;}

/* ── APP BODY ── */
.appbody{display:flex;flex:1;overflow:hidden;}

/* ── ACTIVITY BAR ── */
.actbar{
  width:48px;background:var(--actbar);
  display:flex;flex-direction:column;align-items:center;
  padding-top:0;flex-shrink:0;
  border-right:1px solid var(--border);
}
.ab-item{
  width:48px;height:48px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;position:relative;
  color:rgba(255,255,255,0.4);transition:color .12s;
}
.ab-item:hover{color:rgba(255,255,255,0.9);}
.ab-item.active{color:#ffffff;}
.ab-item.active::before{
  content:'';position:absolute;left:0;top:10px;bottom:10px;
  width:2px;background:#fff;border-radius:0 2px 2px 0;
}
.ab-icon{font-size:20px;line-height:1;}
.ab-badge{
  position:absolute;top:7px;right:7px;
  background:#007acc;color:#fff;
  font-size:9px;font-weight:700;
  min-width:14px;height:14px;
  border-radius:7px;padding:0 3px;
  display:flex;align-items:center;justify-content:center;
}
.ab-bottom{margin-top:auto;margin-bottom:4px;}
.ab-tooltip{
  position:absolute;left:52px;
  background:rgba(80,80,80,0.95);color:#fff;
  font-size:12px;padding:4px 8px;border-radius:3px;
  white-space:nowrap;pointer-events:none;display:none;z-index:100;
}
.ab-item:hover .ab-tooltip{display:block;}

/* ── SIDEBAR ── */
.sidebar{
  width:260px;background:var(--sidebar);
  display:flex;flex-direction:column;
  border-right:1px solid var(--sidebar-border);
  flex-shrink:0;overflow:hidden;transition:width .15s;
}
.sidebar.collapsed{width:0;}
.sb-title{
  height:35px;display:flex;align-items:center;justify-content:space-between;
  padding:0 12px;font-size:11px;font-weight:600;
  letter-spacing:1.2px;text-transform:uppercase;
  color:var(--sidebar-text);flex-shrink:0;
}
.sb-actions{display:flex;gap:2px;}
.sb-btn{
  width:22px;height:22px;border-radius:4px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:14px;
  transition:all .1s;
}
.sb-btn:hover{background:var(--hover-bg);color:var(--sidebar-text);}

/* File tree */
.file-tree{flex:1;overflow-y:auto;overflow-x:hidden;}
.file-tree::-webkit-scrollbar{width:6px;}
.file-tree::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}
.tree-row{
  height:22px;display:flex;align-items:center;
  cursor:pointer;padding-right:8px;font-size:13px;
  color:var(--sidebar-text);position:relative;transition:background .05s;
}
.tree-row:hover{background:var(--sidebar-hover);}
.tree-row.selected{background:var(--sidebar-active);}
.tree-row.selected::before{content:'';position:absolute;left:0;top:0;bottom:0;width:1px;background:#007acc;}
.tree-row.cut{opacity:0.5;}
.tree-indent{flex-shrink:0;}
.tree-arrow{width:16px;flex-shrink:0;font-size:9px;color:var(--sidebar-muted);display:flex;align-items:center;justify-content:center;}
.tree-icon{width:18px;flex-shrink:0;font-size:14px;}
.tree-name{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:13px;}
.tree-row.renaming .tree-name{display:none;}
.rename-input{
  flex:1;background:var(--input-bg);border:1px solid #007acc;
  color:var(--sidebar-text);font-size:13px;padding:0 4px;outline:none;height:18px;
}

/* ── SEARCH SIDEBAR ── */
.search-sb{padding:8px;display:flex;flex-direction:column;gap:6px;flex:1;overflow:hidden;}
.search-row{display:flex;gap:4px;align-items:center;}
.sb-input{
  flex:1;background:var(--input-bg);border:1px solid var(--input-border);
  color:var(--sidebar-text);font-size:12px;padding:4px 8px;outline:none;border-radius:2px;
  font-family:inherit;
}
.sb-input:focus{border-color:#007acc;}
.sb-toggle{
  width:24px;height:24px;border-radius:3px;background:none;border:1px solid transparent;
  color:var(--sidebar-muted);cursor:pointer;font-size:12px;display:flex;align-items:center;justify-content:center;
  transition:all .1s;
}
.sb-toggle:hover{background:var(--hover-bg);color:var(--sidebar-text);}
.sb-toggle.on{background:var(--sidebar-active);color:#fff;border-color:#007acc;}
.search-results{flex:1;overflow-y:auto;font-size:12px;}
.search-results::-webkit-scrollbar{width:4px;}
.search-results::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.sr-file{padding:4px 8px;color:var(--sidebar-text);font-weight:600;cursor:pointer;display:flex;align-items:center;gap:4px;}
.sr-file:hover{background:var(--sidebar-hover);}
.sr-match{
  padding:2px 8px 2px 28px;color:var(--sidebar-muted);cursor:pointer;
  display:flex;gap:4px;align-items:flex-start;
}
.sr-match:hover{background:var(--sidebar-hover);color:var(--sidebar-text);}
.sr-line-num{color:#858585;flex-shrink:0;min-width:28px;text-align:right;}
.sr-text{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.sr-hl{background:rgba(255,200,0,0.3);border-radius:2px;}
.sr-count{font-size:11px;color:var(--sidebar-muted);padding:4px 8px;}

/* ── GIT SIDEBAR ── */
.git-sb{padding:8px;display:flex;flex-direction:column;gap:8px;flex:1;overflow-y:auto;}
.git-commit-area{display:flex;flex-direction:column;gap:6px;}
.git-msg{
  width:100%;background:var(--input-bg);border:1px solid var(--input-border);
  color:var(--sidebar-text);font-size:12px;padding:6px 8px;outline:none;border-radius:2px;
  resize:vertical;min-height:60px;font-family:inherit;
}
.git-msg:focus{border-color:#007acc;}
.git-commit-btn{
  background:var(--btn-bg);color:#fff;border:none;padding:5px 10px;
  border-radius:2px;cursor:pointer;font-size:12px;font-weight:600;
  transition:background .1s;
}
.git-commit-btn:hover{background:var(--btn-hover);}
.git-section{font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--sidebar-muted);padding:4px 0;}
.git-file{
  display:flex;align-items:center;gap:6px;padding:3px 4px;
  border-radius:3px;cursor:pointer;transition:background .07s;
  color:var(--sidebar-text);font-size:12px;
}
.git-file:hover{background:var(--sidebar-hover);}
.git-status{width:14px;font-weight:700;font-size:11px;flex-shrink:0;}
.git-status.M{color:#cca700;}
.git-status.U{color:#89d185;}
.git-status.D{color:#f48771;}
.git-status.A{color:#89d185;}
.git-actions{margin-left:auto;display:flex;gap:2px;opacity:0;transition:opacity .1s;}
.git-file:hover .git-actions{opacity:1;}
.git-act-btn{
  width:18px;height:18px;border-radius:2px;background:none;border:none;
  color:var(--sidebar-muted);cursor:pointer;font-size:11px;display:flex;align-items:center;justify-content:center;
}
.git-act-btn:hover{background:var(--hover-bg);color:var(--sidebar-text);}

/* ── EXTENSIONS SIDEBAR ── */
.ext-list{flex:1;overflow-y:auto;}
.ext-item{
  padding:10px 12px;display:flex;gap:10px;cursor:pointer;
  border-bottom:1px solid var(--border);transition:background .07s;
}
.ext-item:hover{background:var(--sidebar-hover);}
.ext-icon{width:40px;height:40px;border-radius:6px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:22px;}
.ext-info{flex:1;min-width:0;}
.ext-name{font-size:13px;font-weight:600;color:var(--sidebar-text);}
.ext-desc{font-size:11px;color:var(--sidebar-muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:2px;}
.ext-meta{display:flex;gap:6px;margin-top:4px;align-items:center;}
.ext-pub{font-size:11px;color:var(--sidebar-muted);}
.ext-stars{font-size:11px;color:#cca700;}
.ext-install-btn{
  padding:3px 10px;border-radius:2px;background:var(--btn-bg);color:#fff;
  border:none;cursor:pointer;font-size:11px;font-weight:600;white-space:nowrap;
  transition:background .1s;
}
.ext-install-btn:hover{background:var(--btn-hover);}
.ext-install-btn.installed{background:none;border:1px solid var(--input-border);color:var(--sidebar-text);}

/* ── EDITOR ZONE ── */
.edzone{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0;}

/* ── TABS ── */
.tabs-bar{
  height:35px;background:var(--tab-bar);
  display:flex;align-items:flex-end;
  border-bottom:1px solid var(--border);
  overflow-x:auto;flex-shrink:0;
}
.tabs-bar::-webkit-scrollbar{height:2px;}
.tabs-bar::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.tab{
  height:35px;display:flex;align-items:center;gap:6px;
  padding:0 10px;cursor:pointer;border-right:1px solid var(--border);
  white-space:nowrap;flex-shrink:0;position:relative;
  background:var(--tab-inactive);color:rgba(255,255,255,0.45);
  transition:color .1s,background .1s;font-size:13px;
  min-width:80px;max-width:180px;
}
body.light .tab{color:rgba(0,0,0,0.4);}
.tab.active{background:var(--tab-active);color:var(--editor-fg);}
.tab.active::after{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:var(--tab-border);}
.tab:hover:not(.active){background:var(--sidebar-hover);color:var(--editor-fg);}
.tab-icon{font-size:13px;flex-shrink:0;}
.tab-name{flex:1;overflow:hidden;text-overflow:ellipsis;font-size:13px;}
.tab-dirty{width:8px;height:8px;border-radius:50%;background:rgba(255,255,255,0.5);flex-shrink:0;}
.tab.active .tab-dirty{background:var(--editor-fg);}
.tab-x{
  width:18px;height:18px;border-radius:3px;flex-shrink:0;
  display:flex;align-items:center;justify-content:center;
  font-size:14px;color:var(--sidebar-muted);transition:all .1s;
}
.tab:hover .tab-x{color:var(--editor-fg);}
.tab-x:hover{background:rgba(255,255,255,0.15)!important;}
.tab-add{
  width:30px;height:35px;display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:18px;flex-shrink:0;
}
.tab-add:hover{color:var(--editor-fg);}

/* ── BREADCRUMB ── */
.breadcrumb{
  height:22px;background:var(--editor-bg);
  border-bottom:1px solid var(--border);
  display:flex;align-items:center;padding:0 14px;gap:2px;
  font-size:12px;color:var(--sidebar-muted);flex-shrink:0;overflow:hidden;
}
.bc-item{cursor:pointer;padding:0 2px;border-radius:2px;transition:background .1s;}
.bc-item:hover{background:var(--hover-bg);color:var(--editor-fg);}
.bc-sep{color:rgba(255,255,255,0.2);}
body.light .bc-sep{color:rgba(0,0,0,0.2);}
.bc-last{color:var(--editor-fg);}

/* ── EDITOR SPLIT ── */
.split-v{display:flex;flex-direction:column;flex:1;overflow:hidden;}
.editor-group{flex:1;display:flex;overflow:hidden;}

/* ── EDITOR PANE ── */
.editor-pane{flex:1;display:flex;overflow:hidden;position:relative;}
.gutter{
  width:60px;background:var(--editor-bg);flex-shrink:0;
  overflow:hidden;border-right:1px solid transparent;
  display:flex;flex-direction:column;
}
.gutter-nums{
  padding:0 10px 0 4px;
  font-family:'Consolas','Courier New',monospace;
  font-size:var(--font-size);line-height:var(--line-height);
  color:var(--line-num);text-align:right;white-space:pre;
  padding-top:10px;
}
.code-wrap{flex:1;overflow:auto;position:relative;}
.code-wrap::-webkit-scrollbar{width:10px;height:10px;}
.code-wrap::-webkit-scrollbar-track{background:var(--editor-bg);}
.code-wrap::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}
.code-wrap::-webkit-scrollbar-corner{background:var(--editor-bg);}
.code-editor{
  min-height:100%;min-width:100%;width:max-content;
  padding:10px 0;font-family:'Consolas','Courier New',monospace;
  font-size:var(--font-size);line-height:var(--line-height);
  color:var(--editor-fg);background:transparent;
  border:none;resize:none;outline:none;tab-size:4;
  caret-color:#aeafad;white-space:pre;overflow:hidden;
}
.code-editor.wrap{white-space:pre-wrap;width:100%;}

/* ── MINIMAP ── */
.minimap{
  width:80px;background:var(--minimap-bg);
  border-left:1px solid var(--border);flex-shrink:0;
  overflow:hidden;position:relative;cursor:pointer;
}
.mm-viewport{
  position:absolute;left:0;right:0;
  background:rgba(255,255,255,0.08);
  pointer-events:none;min-height:20px;
}
.mm-code{
  padding:4px;font-size:2px;line-height:3px;
  font-family:monospace;white-space:pre;
  overflow:hidden;pointer-events:none;
  color:var(--editor-fg);opacity:0.4;
  transform-origin:top left;
}

/* ── PANEL ── */
.panel{
  background:var(--panel-bg);flex-shrink:0;
  border-top:1px solid var(--border);
  display:flex;flex-direction:column;
  min-height:28px;
}
.panel.closed{height:28px!important;}
.panel-header{
  height:28px;background:var(--panel-header);
  display:flex;align-items:center;
  border-bottom:1px solid var(--border);
  flex-shrink:0;
}
.panel-tabs-wrap{display:flex;align-items:flex-end;flex:1;padding-left:8px;height:100%;}
.ptab{
  height:28px;display:flex;align-items:center;
  padding:0 12px;font-size:11px;font-weight:600;
  letter-spacing:0.5px;text-transform:uppercase;
  color:var(--sidebar-muted);cursor:pointer;
  border-bottom:1px solid transparent;transition:all .1s;
}
.ptab:hover{color:var(--editor-fg);}
.ptab.active{color:var(--editor-fg);border-bottom-color:var(--editor-fg);}
.panel-acts{display:flex;align-items:center;gap:2px;padding:0 8px;margin-left:auto;}
.panel-act{
  width:22px;height:22px;border-radius:4px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--sidebar-muted);font-size:13px;transition:all .1s;
}
.panel-act:hover{background:var(--hover-bg);color:var(--editor-fg);}
.panel-body{flex:1;overflow:hidden;display:flex;flex-direction:column;}
.panel-content{
  flex:1;overflow-y:auto;overflow-x:auto;
  padding:4px 0;
}
.panel-content::-webkit-scrollbar{width:6px;height:6px;}
.panel-content::-webkit-scrollbar-thumb{background:var(--scrollbar);border-radius:2px;}

/* Terminal */
.terminal{
  flex:1;overflow-y:auto;overflow-x:hidden;
  padding:4px 12px;
  font-family:'Consolas','Courier New',monospace;
  font-size:13px;line-height:1.5;color:#cccccc;
}
.terminal::-webkit-scrollbar{width:6px;}
.terminal::-webkit-scrollbar-thumb{background:var(--scrollbar);}
.term-line{white-space:pre-wrap;word-break:break-all;margin:1px 0;}
.term-prompt{color:#4ec9b0;}
.term-ok{color:#89d185;}
.term-err{color:#f48771;}
.term-warn{color:#cca700;}
.term-info{color:#569cd6;}
.term-dim{color:#858585;}
.term-bold{font-weight:700;}
.term-input-row{display:flex;align-items:center;gap:4px;padding:2px 0;}
.term-input{
  flex:1;background:transparent;border:none;outline:none;
  color:#cccccc;font-family:'Consolas','Courier New',monospace;
  font-size:13px;caret-color:#aeafad;
}
.term-tabs{display:flex;gap:0;align-items:center;padding:0 4px;border-bottom:1px solid var(--border);}
.term-tab{
  padding:3px 10px;font-size:12px;color:var(--sidebar-muted);
  cursor:pointer;border-radius:3px 3px 0 0;transition:all .1s;
}
.term-tab:hover{color:var(--editor-fg);}
.term-tab.active{background:var(--panel-bg);color:var(--editor-fg);}
.term-tab-add{padding:3px 8px;color:var(--sidebar-muted);cursor:pointer;font-size:14px;}
.term-tab-add:hover{color:var(--editor-fg);}
.term-split-btn{padding:3px 8px;color:var(--sidebar-muted);cursor:pointer;margin-left:auto;font-size:12px;}
.term-split-btn:hover{color:var(--editor-fg);}

/* Problems */
.problem-item{
  display:flex;align-items:flex-start;gap:6px;
  padding:4px 12px;font-size:12px;curs
.term-tabs{display:flex;gap:0;align-items:center;padding:0 4px;border-bottom:1px solid var(--border);}
.term-tab{
  padding:3px 10px;font-size:12px;color:var(--sidebar-muted);
  cursor:pointer;border-radius:3px 3px 0 0;transition:all .1s;
}
.term-tab:hover{color:var(--editor-fg);}
.term-tab.active{background:var(--panel-bg);color:var(--editor-fg);}
.term-tab-add{padding:3px 8px;color:var(--sidebar-muted);cursor:pointer;font-size:14px;}
.term-tab-add:hover{color:var(--editor-fg);}
.term-split-btn{padding:3px 8px;color:var(--sidebar-muted);cursor:pointer;margin-left:auto;font-size:12px;}
.term-split-btn:hover{color:var(--editor-fg);}

/* Problems */
.problem-item{
  display:flex;align-items:flex-start;gap:6px;
  padding:4px 12px;font-size:12px;curs
