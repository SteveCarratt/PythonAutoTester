import sublime_plugin

TB_FILE = r'[ ]*File \"(...*?)\", line ([0-9]*)'


class PythonContinuousTestRunner(sublime_plugin.EventListener):
    def on_post_save(self, view: sublime_plugin.sublime.View):
        filename = view.file_name()

        if view.is_scratch() or not 'py' == filename[len(filename)-2:len(filename)]:
            return
        if (len(view.window().folders()) == 0):
            return

        wdir = view.window().folders()[0]
        view.window().run_command(
            "exec", {"cmd": ['nose2'],
                     "file_regex": TB_FILE,
                     "shell": True,
                     "quiet": True,
                     "working_dir": wdir})
