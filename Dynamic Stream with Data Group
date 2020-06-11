when HTTP_REQUEST {
	STREAM::disable
	set dynamicStream 0
	if {[class match [HTTP::uri] contains stream_url]} {
		set dynamicStream 1
		set dynamicUri [HTTP::uri]
	}
}

when HTTP_RESPONSE {
	if {$dynamicStream} {
		switch [HTTP::header "Content-Type"] {
			application/javascript -
			text/css -
			application/json -
			text/html {
				set StreamExpr [class match -value $dynamicUri contains stream_url]
				STREAM::max_matchsize 11000000
				STREAM::expression $StreamExpr
				STREAM::enable
			}
		}
	}
}
